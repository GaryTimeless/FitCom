<template>
  <div class="landing-page">
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-title style="text-align: center; width: 100%">Wheyle</ion-title>
        <ion-title style="text-align: center; width: 100%"
          >Die intelligente Wa(h)l für deine Supplements</ion-title
        >
      </ion-toolbar>
    </ion-header>

    <img src="../img/logo.png" alt="Bildbeschreibung 1" class="bottom-image" />
    <ion-title style="text-align: center; width: 100%; font-size: x-large;">Compare fitness supplements across companies.</ion-title>
    <ion-title style="text-align: center; width: 100%; font-size: small;">Start with a pre-selected selection by clicking on one of the product categories</ion-title>

    <div class="products-section">
      <button
        class="product-button"
        v-for="product in filteredProducts"
        :key="product.id"
        @click="selectProduct(product)"
      >
        {{ product.name }}
      </button>
      
      
    </div>
    <button class="product-button-all" @click="allProducts">
        show me all products at once
      </button>
  </div>
</template>

<script lang="ts">
import router from "@/router";
import { defineComponent, ref, computed } from "vue";

interface Product {
  id: number;
  name: string;
}

export default defineComponent({
  name: "LandingPage",
  setup() {
    const searchTerm = ref("");
    const products = ref<Product[]>([
      { id: 1, name: "Protein" },
      { id: 2, name: "Clear Whey" },
      { id: 3, name: "Creatine" },
      // Fügen Sie hier weitere Produkte hinzu
    ]);

    const filteredProducts = computed(() => {
      if (searchTerm.value) {
        return products.value.filter((product) =>
          product.name.toLowerCase().includes(searchTerm.value.toLowerCase())
        );
      }
      return products.value;
    });
const allProducts =()=>{
  router.push({ name: "FitCom" });

}
    const selectProduct = (product: Product) => {
      // Logik zum Auswählen eines Produkts
      console.log("Produkt ausgewählt:", product.name);
      // Fügen Sie hier die Navigation zur Detailseite hinzu, falls benötigt
      // router.push({ name: 'FitCom' });
      router.push({ name: "FitCom", query: { productCategory: product.name } });
    };

    return { searchTerm, filteredProducts, selectProduct,allProducts };
  },
});
</script>

<style scoped>
/* Hier fügen Sie Ihre CSS-Stile hinzu, wie oben definiert */

.landing-page {
  display: flex;
  flex-direction: column;
  align-items: center;
  /* Zusätzliche Stile für das Layout der Landing Page */
}

.products-section {
  margin-top: 20px;
}

.product-button {
  padding: 10px 20px; /* Oben/Unten, Rechts/Links */
  font-size: 16px; /* Oder die gewünschte Schriftgröße */
  margin: 5px; /* Abstand zwischen den Buttons */
  border: 1px solid #ccc; /* Rahmen um den Button */
  background-color: #52e1f7; /* Hintergrundfarbe */
  cursor: pointer; /* Zeiger, um anzuzeigen, dass der Button klickbar ist */
  /* Weitere Stile wie Schriftart, Rundung der Ecken etc. */
  border-radius: 5px; /* Rundung der Ecken */
  min-width: 190px; /* Minimale Breite */
  min-height: 60;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.2); /* Schatten für eine bessere Tiefe */
  transition: all 0.3s ease; /* Eine sanfte Übergangsanimation */
}

.product-button-all {
  padding: 10px 20px; /* Oben/Unten, Rechts/Links */
  font-size: 16px; /* Oder die gewünschte Schriftgröße */
  margin-top: 30px; /* Abstand zwischen den Buttons */
  border: 1px solid #909090; /* Rahmen um den Button */
  background-color: #3dabbc; /* Hintergrundfarbe */
  cursor: pointer; /* Zeiger, um anzuzeigen, dass der Button klickbar ist */
  /* Weitere Stile wie Schriftart, Rundung der Ecken etc. */
  border-radius: 5px; /* Rundung der Ecken */
  min-width: 190px; /* Minimale Breite */
  min-height: 60;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.2); /* Schatten für eine bessere Tiefe */
  transition: all 0.3s ease; /* Eine sanfte Übergangsanimation */
}

.product-button:hover {
  background-color: #e0e0e0; /* Farbwechsel beim Hover */
  box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.3); /* Größerer Schatten beim Hover */
}
</style>
