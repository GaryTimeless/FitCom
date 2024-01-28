<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-title style="text-align: center; width: 100%;">Wheyle</ion-title>
        <ion-title style="text-align: center; width: 100%;">Die intelligente Wa(h)l für deine Supplements</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true">
      <ion-refresher slot="fixed" @ionRefresh="refresh($event)">
        <ion-refresher-content></ion-refresher-content>
      </ion-refresher>

      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Inbox</ion-title>
        </ion-toolbar>
      </ion-header>
       <!-- Bilder Sektion -->
       <div class="image-section">
        <div class="image-stack">
          <img src="../img/logo.png" alt="Bildbeschreibung 1" class="bottom-image">
          
        </div>
      </div>
      <!-- Filter & Liste Sektion -->
      <div class="Container">
       

        <!-- List of all Filter-->
        <div class="filter-wrapper">
          <ion-list>
            <!-- Firma Filter -->
            <FirmaFilter
              :firmen="firmenListe"
              @SelectedFirmaChange="handleSelectedFirmen"
            />

            <ProduktkategorieFilter
              :productKategorie="productKategorieListe"
              :initialValue="initialSelectedKategorie"
              @SelectedProduktKategorieChange="handleSelectedProduktKategorie"
            />

            <PriceRangeFilter @validMaxPrice="handleValidMaxPrice" />

            <!-- VEGAN-->
            <veganFilter @update:modelValue="handleVeganChange" />

            <PakgSizeFilter @selectedPakgSize="handleSelectedPakgSize" />
          </ion-list>
        </div>

        <!-- List of all Products-->
        <div class="list-wrapper">
          <ion-list>
            <FitProductCategoryButton
              @sort="sortProducts"
            ></FitProductCategoryButton>
            <FitProductListItem
            class="FPLI-flexControll"
              v-for="product in filteredProducts"
              :key="product.id"
              :product="product"
            />
          </ion-list>
        </div>
      </div>
      <!-- improvised footer-->
      <div
        style="
          height: 100px;
          background-color: rgb(66, 58, 50);
          margin-top: 10%;
        "
      ></div>
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import PakgSizeFilter from "@/components/Filter/PakgSizeFilter.vue";
const SelectedPakgSizeFromChild = ref<{ lower: number; upper: number }>({
  lower: 0,
  upper: 0,
});
const handleSelectedPakgSize = (PakgSize: any) => {
  SelectedPakgSizeFromChild.value.lower = PakgSize.value.lower;
  SelectedPakgSizeFromChild.value.upper = PakgSize.value.upper;
};

import {
  IonContent,
  IonHeader,
  IonList,
  IonPage,
  IonRefresher,
  IonRefresherContent,
  IonTitle,
  IonToolbar,
} from "@ionic/vue";
import FitProductListItem from "@/components/FitProductListItem.vue";
import FitProductCategoryButton from "@/components/FitProductCategoryButton.vue";
import { FitProduct } from "@/data/FitProducts";

import { watch, ref, onMounted, computed, Ref } from "vue";

declare var gapi: any;

const products = ref<FitProduct[]>([]);

type ProduktKategorieType = {
  value: string;
  label: string;
};
// Zustand für die Initialisierung von gapi
const gapiInitialized = ref(false);
const initialSelectedKategorie = ref<ProduktKategorieType | null>(null); // Definieren Sie es als ref<string>

const route = useRoute();
// Initialisiere gapi, wenn die Seite geladen wird
onMounted(() => {
  if (typeof gapi !== "undefined") {
    gapi.load("client", () => {
      gapi.client
        .init({
          apiKey: "AIzaSyB8SicDdK4Y13FgWJ9FP_SPg3ApT5rXCD0",
          discoveryDocs: [
            "https://sheets.googleapis.com/$discovery/rest?version=v4",
          ],
        })
        .then(() => {
          gapiInitialized.value = true;
        });
    });
  }
  const queryCategory = route.query.productCategory as string | undefined;
  if (queryCategory) {
    handleSelectedProduktKategorie([queryCategory]);
    initialSelectedKategorie.value = {
      value: queryCategory,
      label: queryCategory,
    };
    console.log(initialSelectedKategorie);
    console.log("_____");
  }
});

function fetchProductsFromSheet() {
  if (!gapiInitialized.value) return;

  gapi.client.sheets.spreadsheets.values
    .get({
      spreadsheetId: "1P2hq9-DQkitIYaZFzSh6av_2uP-ifk529yZbNfGZV4U",
      range: "Base",
    })
    .then((response: any) => {
      const rawData = response.result.values;
      products.value = rawData.slice(1).map((row: any) => ({
        firma: row[0],
        produktkategorie: row[1],
        name: row[2],
        vegan: row[3],
        preisPerPackung: row[4],
        preisPerKG: row[5],
        portionierung: row[6],
        portionenPerPkg: row[7],
        gewichtPerPkg: row[10],
      }));

      const uniqueFirmen = [
        ...new Set(products.value.map((product) => product.firma)),
      ];
      const uniqueProduktKategorien = [
        ...new Set(products.value.map((product) => product.produktkategorie)),
      ];

      // Aktualisiere firmenListe
      firmenListe.value = uniqueFirmen.map((firma) => ({
        value: firma,
        label: firma,
      }));

      // Aktualisiere productKategorieListe
      productKategorieListe.value = uniqueProduktKategorien.map(
        (kategorie) => ({ value: kategorie, label: kategorie })
      );
    });
}

// Rufe die Funktion auf, sobald gapi initialisiert ist
watch(gapiInitialized, (newValue) => {
  if (newValue) fetchProductsFromSheet();
});

watch(
  () => route.query.productCategory,
  (queryCategory) => {
    if (queryCategory) {
      initialSelectedKategorie.value = {
        value: queryCategory as string,
        label: queryCategory as string,
      };
    }
  },
  { immediate: true }
);

// const products = ref<FitProduct[]>(getProducts());

const refresh = (ev: CustomEvent) => {
  setTimeout(() => {
    ev.detail.complete();
  }, 3000);
};

//TODO Test entfernen?
const Test = (selectedFirma: string[]) => {
  // Hier erhältst du die ausgewählten Firmen von der Kindkomponente
  console.log(
    "Ausgewählte Firmen in übergeordneter Komponente:",
    selectedFirma
  );

  // Verarbeite die ausgewählten Firmen hier
};

const sortProducts = (key: string) => {
  console.log(key + "next");

  if (key === "Firma") {
    products.value.sort((a, b) => a.firma.localeCompare(b.firma));
  }
  if (key === "Kategorie") {
    products.value.sort((a, b) =>
      a.produktkategorie.localeCompare(b.produktkategorie)
    );
  }
  if (key === "Preis/Pkg") {
    //products.value.sort((a, b) => a.preisPerKG - b.preisPerKG);
    products.value.sort((a, b) => {
      const numA = parseFloat(a.preisPerPackung);
      const numB = parseFloat(b.preisPerPackung);
      return numA - numB;
    });

    console.log(products);
  }
  if (key === "PreisProKG") {
    products.value.sort((a, b) => a.preisPerKG - b.preisPerKG);
    console.log(products);
  }
  if (key === "Produktname") {
    products.value.sort((a, b) => a.name.localeCompare(b.name));
  }
  if (key === "Portionierung") {
    products.value.sort((a, b) => a.portionierung - b.portionierung);
  }
  if (key === "PortionenPerPkg") {
    products.value.sort((a, b) => a.portionenPerPkg - b.portionenPerPkg);
  }
  if (key === "GewichtPerPkg") {
    products.value.sort((a, b) => {
      const numA = parseFloat(a.gewichtPerPkg);
      const numB = parseFloat(b.gewichtPerPkg);
      return numA - numB;
    });
  }
  if (key === "Vegan") {
    products.value.sort((a, b) => {
      if (a.vegan === "yes" && b.vegan !== "yes") return -1; // "yes" kommt zuerst
      if (b.vegan === "yes" && a.vegan !== "yes") return 1; // "yes" kommt zuerst

      if (a.vegan === "no" && b.vegan === "no Info") return -1; // "no" vor "no info"
      if (a.vegan === "no Info" && b.vegan === "no") return 1; // "no" vor "no info"

      return 0; // Standardrückgabe, falls keine anderen Bedingungen zutreffen
    });
  }
};

const isVegan = ref(false);
const productType = ref("");
const packSize = ref({ lower: 100, upper: 2000 });

import FirmaFilter from "../components/Filter/FirmaFilter.vue";
import ProduktkategorieFilter from "../components/Filter/ProduktkategorieFilter.vue";

//TODO Dummies austauschen? Die Frage ist hier oder in der Ecxel auf nem zweiten sheet?

const firmenListe: Ref<Firma[]> = ref([]);

type Firma = { value: string; label: string };
const selectedFirmenFromChild = ref<Firma[]>([]);

const handleSelectedFirmen = (selectedFirma: string[]) => {
  console.log("Selected firms:", selectedFirma);
  const selectedFirmenAsObjects: Firma[] = selectedFirma.map((firma) => ({
    value: firma,
    label: firma, // Du kannst den Wert von 'label' anpassen, falls erforderlich
  }));
  selectedFirmenFromChild.value = selectedFirmenAsObjects;
};

type ProduktKategorie = { value: string; label: string };
const selectedProduktKategorieFromChild = ref<ProduktKategorie[]>([]);

const handleSelectedProduktKategorie = (
  SelectedProduktKategorieChange: string[]
) => {
  console.log("Selected ProduktKategorie:", SelectedProduktKategorieChange);
  const selectedProduktKategorieAsObjects: ProduktKategorie[] =
    SelectedProduktKategorieChange.map((produktKategorie) => ({
      value: produktKategorie,
      label: produktKategorie, // Du kannst den Wert von 'label' anpassen, falls erforderlich
    }));
  selectedProduktKategorieFromChild.value = selectedProduktKategorieAsObjects;
};

const filteredProducts = computed(() => {
  // Wenn alle Filter deaktiviert sind
  if (
    selectedFirmenFromChild.value.length === 0 &&
    selectedProduktKategorieFromChild.value.length === 0 &&
    selectedMaxPriceFromChild.value === null &&
    !isCheckedref.value &&
    SelectedPakgSizeFromChild.value.lower === 0 &&
    SelectedPakgSizeFromChild.value.upper === 0
  ) {
    console.log("All Filter Off: First time?");
    return products.value;
  }

  return products.value.filter((product) => {
    const gewichtAsNumber = parseInt(product.gewichtPerPkg, 10);

    const isFirmValid =
      selectedFirmenFromChild.value.length === 0 ||
      selectedFirmenFromChild.value.some(
        (firma) => firma.value === product.firma
      );

    const isProductCategoryValid =
      selectedProduktKategorieFromChild.value.length === 0 ||
      selectedProduktKategorieFromChild.value.some(
        (kategorie) => kategorie.value === product.produktkategorie
      );

    const isPriceValid =
      selectedMaxPriceFromChild.value === null ||
      product.preisPerKG <= selectedMaxPriceFromChild.value;

    const isVeganValid = !isCheckedref.value || product.vegan == "yes";

    const isPakgSizeValid =
      (SelectedPakgSizeFromChild.value.lower === 0 &&
        SelectedPakgSizeFromChild.value.upper === 0) ||
      (gewichtAsNumber >= SelectedPakgSizeFromChild.value.lower &&
        gewichtAsNumber <= SelectedPakgSizeFromChild.value.upper);

    return (
      isFirmValid &&
      isProductCategoryValid &&
      isPriceValid &&
      isVeganValid &&
      isPakgSizeValid
    );
  });
});

const productKategorieListe = ref([
  { value: "Protein", label: "Protein" },
  { value: "Creatine", label: "Kreatine" },
  // TODO weitere Optionen
  //TODO überflüssig geworden?
]);

import PriceRangeFilter from "../components/Filter/PriceRangeFilter.vue";
const selectedMaxPriceFromChild = ref<number | null>(null);
const handleValidMaxPrice = (maxPrice: string) => {
  // Speichere den Wert in selectedMaxPriceFromChild
  selectedMaxPriceFromChild.value = parseFloat(maxPrice.replace(",", "."));
};

const handleVeganChange = (value: any) => {
  isCheckedref.value = value;
  // Führe hier weitere Aktionen basierend auf dem geänderten Wert aus
};
const isCheckedref = ref(false);

import veganFilter from "@/components/Filter/veganFilter.vue";
import { useRoute } from "vue-router";
// const selectedIsVeganFromChild = ref<boolean>(false);

// console.log("Übertrag hat geklappt. "+isChecked.value + typeof isChecked)
// selectedIsVeganFromChild.value =isChecked
// console.log("Ütest. "+selectedIsVeganFromChild.value)
</script>

<style scoped>

.image-section {
  text-align: center; /* Zentriert die Bilder */
  position: relative; /* Position relativ für das Bild-Stacking */
  margin-bottom: 20px; /* Abstand zwischen den Bildern und dem Filter-Container */
}

.image-stack {
  display: inline-block; /* Damit der Container nur so breit wie die Bilder ist */
  position: relative;
}

.bottom-image, .top-image {
  /* position: absolute; */
  top: 0;
  left: 50%; 
  /* Zentriert die Bilder horizontal */
/* transform: translateX(-50%);  */
/* Korrigiert die Zentrierung unter Berücksichtigung der Bildbreite */
}

.top-image {
z-index: 1; /* Stellt sicher, dass das Bild oben liegt */
}


.Container {
  display: flex;
  align-items: start;
  background-color: #fff;
}
.filter-wrapper {
  flex: 0 0 25%;
  padding-right: 1rem;
  flex-basis: calc(
    25% - 60px
  ); /* Nimmt 25% der Breite minus 60px (30px auf jeder Seite) ein */
  margin: 0% 0 0 5%;
}

.pckLabel {
  --label-width: 150px; /* oder ein anderer geeigneter Wert */
  padding-bottom: 5px;
}

.list-wrapper {
  display: flex;
  overflow-x: auto;
  flex-wrap: nowrap;
  margin-top: 0%;
  margin-right: 10%;
  flex: 1; /* Nimmt den verbleibenden Raum ein */
  overflow-x: auto;
}

@media (prefers-color-scheme: dark) {
  .Container {
    background-color: #1e1e1e; /* Dunkle Hintergrundfarbe für Dark Mode */
    color: #ffffff; /* Helle Schriftfarbe für Dark Mode */
  }
}

@media (prefers-color-scheme: light), (prefers-color-scheme: no-preference) {
  .Container {
    background-color: #fff; /* Helle Hintergrundfarbe für Light Mode */
    color: #000000; /* Dunkle Schriftfarbe für bessere Lesbarkeit im Light Mode */
  }
}
.filter-wrapper ion-label {
  margin: 0; /* Entfernt den Margin */
}

ion-range::part(tick) {
  background: #a2d2ff;
}

ion-range::part(tick-active) {
  background: #bde0fe;
}

ion-range::part(pin) {
  display: inline-flex;
  align-items: center;
  justify-content: center;

  background: #ffafcc;
  color: #fff;

  border-radius: 50%;
  transform: scale(1.01);

  top: -20px;

  min-width: 28px;
  height: 28px;
  transition:
    transform 120ms ease,
    background 120ms ease;
}

ion-range::part(pin)::before {
  content: none;
}

ion-range::part(knob) {
  background: #ffc8dd;
}

ion-range::part(bar) {
  background: #a2d2ff;
}

ion-range::part(bar-active) {
  background: #bde0fe;
}
.FPLI-flexControll{
  display: flex;
  flex-wrap: nowrap;
}
</style> -->
