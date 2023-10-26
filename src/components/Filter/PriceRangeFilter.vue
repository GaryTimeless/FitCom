 <template>
  <div class="price-range">
    <ion-item>
      <ion-label position="stacked">Höchstpreis für 1000g</ion-label>
      <ion-input
        type="number"
        @ionInput="validateMaxPrice($event)"
      ></ion-input>
    </ion-item>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import { IonInput, IonAlert } from "@ionic/vue";
const emit = defineEmits();
const validateMaxPrice = (ev: any) => {
    console.log("TEST?")
  const selectMaxPrice = ev.target.value;
  if (selectMaxPrice !== null && selectMaxPrice < 0) {
    const alert = this.$refs.alert;

    alert.header = "Ungültige Zahl";
    alert.message = "Bitte nur sinnvolle Zahlen eingeben";
    alert.buttons = ["OK"];

    alert.present();
    
  } else {
    // Hier können Sie die gültige Höchstpreis-Eingabe verarbeiten, z.B.:
    emit("validMaxPrice", selectMaxPrice);
    console.log("max price Set to: " + selectMaxPrice);
  }
}
export default defineComponent({
  props: {
    maxPrice: Number,
  },
  data() {
  },
  methods: {
    validateMaxPrice, // Verwenden Sie die oben definierte Funktion
  },
});
</script>

<style scoped></style>

<!-- <ion-alert
      ref="alert"
      v-model="isAlertOpen"
      header="Benachrichtigung"
      message="Dies ist eine Beispiel-Benachrichtigung."
      :buttons="alertButtons"
    ></ion-alert> -->
