<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Welcome to Wheyle</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content class="ion-padding">
      <div class="hero-section">
        <img src="../img/logoold.png" alt="logo wheyle" class="logo" />
        <h2>Die intelligente Wa(h)l für deine Supplements</h2>
        <p class="intro-text">
          Unsere topaktuelle, markenübergreifende Auswahl zeigt dir die 5 besten
          Produkte aus über 30 Angeboten<br />–<br />perfekt für deine
          Fitnessziele und dein Budget.
        </p>
      </div>
      <h1 class="section-title">Protein</h1>
      <p class="section-subtitle">Preis ist in € / 1g Protein pro Portion</p>

      <MyCard
        name="Designer Protein whey"
        firma="ESN"
        content="High quality whey protein for your muscles."
        imageSrc="src/img/ProteinExample.jpg"
        price="0,03"
        :moreInfoAcc="{
          '100g': [
            { label: 'Kcal', value: '300' },
            { label: 'Kohlenhydrate', value: '20g' },
            { label: 'Zucker', value: '2g' },
            { label: 'Eiweiß', value: '80g' },
            { label: 'Fett', value: '0,1g' },
          ],
          portion: [
            { label: 'Kcal', value: '150' },
            { label: 'Kohlenhydrate', value: '10g' },
            { label: 'Zucker', value: '1g' },
            { label: 'Eiweiß', value: '40g' },
            { label: 'Fett', value: '0,05g' },
          ],
          portionSize: '40g',
        }"
      />
      <MyCard
        name="Vegan Whey"
        firma="DM"
        content="really nice and tasty product for every day"
        price="0,04"
        moreInfoAcc="Pro 100g: Kcal 300 | Kohlenhydrate 20g | Zucker 2g | Eiweis 80g | Fett 0,1g "
      />
      <MyCard
        name="Vegan Whey Pro"
        firma="bulk"
        content="for athlete sports persons"
        price="0,05"
        moreInfoAcc="Pro 100g: Kcal 300 | Kohlenhydrate 20g | Zucker 2g | Eiweis 80g | Fett 0,1g "
      />
      <ion-footer>
        <p>&copy; 2024 FitCom. All rights reserved.</p>
      </ion-footer>
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import { ref } from "vue";
import MyCard from "@/components/MyCard.vue";

const message = ref("Hello World");

function navigateToDetails() {
  console.log(message.value);
}
</script>

<style scoped>
.hero-section {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
}

.logo {
  max-width: 80%;
  max-height: 50vh;
  object-fit: contain;
  margin-bottom: 20px;
}

h2 {
  margin-top: 10px;
  font-size: 1.5em;
}

.intro-text {
  font-size: 1em;
  margin-bottom: 20px; /* Fester Abstand zur nächsten Komponente */
  color: #666;
  text-align: center;
}

/* Feste Abstände für Titel und Untertitel */
.section-title {
  text-align: center;
  margin-bottom: 10px;
}

.section-subtitle {
  text-align: center;
  margin-bottom: 20px;
}

ion-footer {
  text-align: center;
  padding: 10px 0;
  font-size: 0.9em;
  color: gray;
}
</style>
