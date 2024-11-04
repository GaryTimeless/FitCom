<template>
  <ion-card class="responsive-card">
    <ion-img v-if="imageSrc" :src="imageSrc" alt="Card Image"></ion-img>
    <ion-card-header>
      <ion-card-title class="company-name">{{ firma }}</ion-card-title>
      <ion-card-subtitle class="product-name">{{ name }}</ion-card-subtitle>
    </ion-card-header>

    <!-- Verwendung von ion-grid, um Inhalt und Preis besser zu strukturieren -->
    <ion-card-content>
      <ion-grid>
        <ion-row>
          <ion-col size="9" class="content-text">
            {{ content }}
          </ion-col>
          <ion-col size="3" class="price-column" text-right>
            <div class="price" v-if="price">{{ price }} €</div>
          </ion-col>
        </ion-row>
      </ion-grid>
    </ion-card-content>
  </ion-card>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import { IonCard, IonCardContent, IonCardHeader, IonCardSubtitle, IonCardTitle, IonImg, IonGrid, IonRow, IonCol } from '@ionic/vue';

export default defineComponent({
  name: 'MyCard',
  components: { IonCard, IonCardContent, IonCardHeader, IonCardSubtitle, IonCardTitle, IonImg, IonGrid, IonRow, IonCol },
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

/* Stil für das Content-Grid */
.content-text {
  font-size: 1em;
  color: #666;
  text-align: justify;
}

/* Stil für die Preis-Spalte */
.price-column {
  display: flex;
  align-items: flex-end;
  justify-content: flex-end;
}

.price {
  font-size: 1.1em;
  font-weight: bold;
  color: #f0f0f0;
  opacity: 0.8;
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