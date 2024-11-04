<template>
  <ion-card>
    <ion-img v-if="imageSrc" :src="imageSrc" alt="Card Image"></ion-img>
    <ion-card-header>
      <ion-card-subtitle class="manufacturer">{{ subtitle }}</ion-card-subtitle>
      <ion-card-title class="product-name">{{ title }}</ion-card-title>
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
    title: {
      type: String,
      default: 'Default Product Name'
    },
    subtitle: {
      type: String,
      default: 'Default Manufacturer'
    },
    content: {
      type: String,
      default: 'Default content for the card.'
    },
    imageSrc: {
      type: String,
      default: '' // Leerer Standardwert, falls kein Bild angegeben ist
    }
  }
});
</script>

<style scoped>
/* Stil für den Herstellernamen */
.manufacturer {
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
</style>