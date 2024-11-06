<template>
  <ion-card class="responsive-card">
    <ion-img v-if="imageSrc" :src="imageSrc" alt="Card Image"></ion-img>
    <ion-card-header>
      <ion-card-title class="company-name">{{ firma }}</ion-card-title>
      <ion-card-subtitle class="product-name">{{ name }}</ion-card-subtitle>
    </ion-card-header>

    <ion-card-content>
      <div class="content-container">
        <div class="content-text">
          {{ content }}
        </div>
        <div class="price" v-if="price">{{ price }} €</div>
      </div>

      <ion-accordion-group>
        <ion-accordion>
          <ion-item slot="header" color="light">
            <ion-label>Mehr Details</ion-label>
          </ion-item>
          <div slot="content">
            <!-- Segment to toggle between "pro 100g" and "pro Portion" -->
            <ion-segment v-model="selectedSegment" value="100g">
              <ion-segment-button value="100g">
                <ion-label>Pro 100g</ion-label>
              </ion-segment-button>
              <ion-segment-button value="portion">
                <ion-label>Pro Portion </ion-label>
              </ion-segment-button>
            </ion-segment>

            <p class="nutritional-header">
              Nährwerte
              {{
                selectedSegment === "100g"
                  ? "pro 100g"
                  : `pro Portion (${portionSize.value})`
              }}
            </p>

            <table class="product-details-table">
              <tr
                v-for="(detail, index) in displayedNutritionalValues"
                :key="index"
              >
                <td>{{ detail.label }}:</td>
                <td>{{ detail.value }}</td>
              </tr>
            </table>
          </div>
        </ion-accordion>
      </ion-accordion-group>
    </ion-card-content>
  </ion-card>
</template>

<script lang="ts">
import { defineComponent, ref, computed } from "vue";
import {
  IonCard,
  IonCardContent,
  IonCardHeader,
  IonCardSubtitle,
  IonCardTitle,
  IonImg,
  IonAccordion,
  IonItem,
  IonLabel,
  IonAccordionGroup,
  IonSegment,
  IonSegmentButton,
} from "@ionic/vue";

// Interface für die Details
interface ProductDetail {
  label: string;
  value: string;
}

export default defineComponent({
  name: "MyCard",
  components: {
    IonCard,
    IonCardContent,
    IonCardHeader,
    IonCardSubtitle,
    IonCardTitle,
    IonImg,
    IonAccordion,
    IonItem,
    IonLabel,
    IonAccordionGroup,
    IonSegment,
    IonSegmentButton,
  },
  props: {
    firma: String,
    name: String,
    content: String,
    imageSrc: String,
    price: [String, Number],
    moreInfoAcc: {
      type: Array as PropType<{
        "100g": ProductDetail[];
        portion: ProductDetail[];
      }>,
      default: () => ({
        "100g": [
          { label: "Kcal", value: "300" },
          { label: "Kohlenhydrate", value: "20g" },
          { label: "Zucker", value: "2g" },
          { label: "Eiweiß", value: "80g" },
          { label: "Fett", value: "0,1g" },
        ],
        portion: [
          { label: "Kcal", value: "150" },
          { label: "Kohlenhydrate", value: "10g" },
          { label: "Zucker", value: "1g" },
          { label: "Eiweiß", value: "40g" },
          { label: "Fett", value: "0,05g" },
        ],
        portionSize: "40g",
      }),
    },
  },
  setup(props) {
    const selectedSegment = ref("100g");

    // Computed property to dynamically return nutritional values based on selected segment
    const displayedNutritionalValues = computed(() => {
      return props.moreInfoAcc[selectedSegment.value];
    });

    // Computed property for portion size
    const portionSize = computed(() => props.moreInfoAcc.portionSize);

    return {
      selectedSegment,
      displayedNutritionalValues,
      portionSize,
    };
  },
});
</script>

<style scoped>
.product-details-table {
  width: 100%;
  border-spacing: 0 5px;
  font-size: 0.9em;
}

.product-details-table td {
  padding: 4px 8px;
  color: #666;
}

.product-details-table td:first-child {
  font-weight: bold;
  text-align: left;
}

.nutritional-header {
  margin: 5px 0;
  font-size: 1em;
  font-weight: bold;
}

.company-name {
  font-size: 0.9em;
  color: gray;
}

.product-name {
  font-size: 1.5em;
  font-weight: bold;
}

ion-img {
  max-width: 100%;
  height: auto;
  object-fit: cover;
  border-radius: 8px 8px 0 0;
}

.content-container {
  position: relative;
  padding-bottom: 20px;
}

.content-text {
  font-size: 1em;
  color: #666;
  text-align: justify;
  margin-bottom: 20px;
  width: 80%;
}

.price {
  position: absolute;
  bottom: 10px;
  right: 10px;
  font-size: 1.2em;
  font-weight: bold;
  color: #e0e0e0;
  opacity: 0.9;
}

.responsive-card {
  width: 100%;
  max-width: 600px;
  margin: auto;
  margin-bottom: 5px;
}

@media (min-width: 768px) {
  .responsive-card {
    width: 80%;
  }
}

@media (min-width: 1024px) {
  .responsive-card {
    width: 60%;
  }
}
</style>
