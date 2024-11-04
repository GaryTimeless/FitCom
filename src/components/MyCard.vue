<template>
  <ion-card class="responsive-card">
    <ion-img v-if="imageSrc" :src="imageSrc" alt="Card Image"></ion-img>
    <ion-card-header>
      <ion-card-title class="company-name">{{ firma }}</ion-card-title>
      <ion-card-subtitle class="product-name">{{ name }}</ion-card-subtitle>
    </ion-card-header>

    <!-- Entfernt das ion-grid und verwendet stattdessen eine content-container-Div -->
    <ion-card-content>
      <div class="content-container">
        <div class="content-text">
          {{ content }}
        </div>
        <div class="price" v-if="price">{{ price }} €</div>
      </div>
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
    },
    price: {
      type: [String, Number],
      default: ''
    }
  }
});
</script>

<style scoped>
/* Stil für den Firmennamen *//* Stil für das ion-card-content, um unerwünschtes Padding zu entfernen */
ion-card-content {
  padding-left: 16px; /* Gleicher linker Abstand wie der Produktname */
  padding-right: 16px; /* Gleicher rechter Abstand */
}

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

/* Blocksatz für den Text */
.content-container {
  padding-bottom: 20px; /* Platz für den Preis am unteren Rand */
  position: relative;
}

.content-text {
  font-size: 1em;
  color: #666;
  text-align: justify;
  margin-bottom: 20px; /* Abstand zum Preis */
  width: 80%;
}

/* Stil für die Preis-Spalte */
.price {
  position: absolute;
  bottom: 10px;
  right: 10px;
  font-size: 1.2em;
  font-weight: bold;
  color: #e0e0e0; /* Heller für bessere Sichtbarkeit */
  opacity: 0.9;
}

/* Responsive Design für die Card */
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