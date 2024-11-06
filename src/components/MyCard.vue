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
            <table class="product-details-table">
              <p style="margin: 5px 5px 5px 5px;">Nährwerte pro 100g</p>
              <tr v-for="(detail, index) in moreInfoAcc" :key="index">
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
import { defineComponent, PropType } from 'vue';
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
  IonAccordionGroup
} from '@ionic/vue';

// Interface für die Details
interface ProductDetail {
  label: string;
  value: string;
}

export default defineComponent({
  name: 'MyCard',
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
    IonAccordionGroup
  },
  props: {
    firma: String,
    name: String,
    content: String,
    imageSrc: String,
    price: [String, Number],
    moreInfoAcc: {
      type: Array as PropType<ProductDetail[]>,
      default: () => []
    }
  }
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