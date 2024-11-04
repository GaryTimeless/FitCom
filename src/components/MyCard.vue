<template>
  <ion-card class="responsive-card">
    <ion-img v-if="imageSrc" :src="imageSrc" alt="Card Image"></ion-img>
    <ion-card-header>
      <ion-card-title class="company-name">{{ firma }}</ion-card-title>
      <ion-card-subtitle class="product-name">{{ name }}</ion-card-subtitle>
    </ion-card-header>

    <ion-card-content>
      {{ content }}
    </ion-card-content>
  </ion-card>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import { IonCard, IonCardContent, IonCardHeader, IonCardSubtitle, IonCardTitle, IonImg } from '@ionic/vue';

export default defineComponent({
  name: 'MyCard',
  components: { IonCard, IonCardContent, IonCardHeader, IonCardSubtitle, IonCardTitle, IonImg },
  props: {
    firma: {
      type: String,
      default: 'Default Company Name'
    },
    name: {
      type: String,
      default: 'Default Product Name'
    },
    content: {
      type: String,
      default: 'Default content for the card.'
    },
    imageSrc: {
      type: String,
      default: ''
    }
  }
});
</script>

<style scoped>
/* Stil für den Firmennamen */
.company-name {
  font-size: 0.9em;
  color: gray;
}

/* Stil für den Produktnamen */
.product-name {
  font-size: 1.5em;
  font-weight: bold;
}

/* Stil für das Bild */
ion-img {
  max-width: 100%;
  height: auto;
  object-fit: cover;
  border-radius: 8px 8px 0 0;
}

/* Responsive Design für die Card */
.responsive-card {
  width: 100%; /* Standard für mobile Bildschirme */
  max-width: 600px; /* Maximale Breite auf größeren Bildschirmen */
  margin: auto; /* Zentriert die Karte auf dem Bildschirm */
  margin-bottom: 5px;
}

@media (min-width: 768px) {
  /* Ab Tablet-Breite wird die Karte schmaler dargestellt */
  .responsive-card {
    width: 80%;
  }
}

@media (min-width: 1024px) {
  /* Ab Desktop-Breite wird die Karte weiter begrenzt */
  .responsive-card {
    width: 60%;
  }
}
</style>