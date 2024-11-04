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
            <br>Unsere topaktuelle, markenübergreifende Auswahl zeigt dir die 5 besten Produkte 
            aus über 30 Angeboten</br> <br>–</br><br>perfekt für deine Fitnessziele und dein Budget.</br>
        </p>
      </div>
      <h1 style="text-align: center;">Protein</h1>
      <p style="text-align: center;">Preis ist in € / 1g Protein pro Portion</p>

      <MyCard
        name="Designer Protein whey"
        firma="ESN"
        content="High quality whey protein for your muscles.High quality whey protein for your muscles. High quality and tatsy whey protein for your muscles. This is High quality whey protein for your muscles."
        imageSrc="src/img/ProteinExample.jpg"
        price="0,03"
        style="margin-bottom: 20px"
      />
      <MyCard
        name="Vegan Whey"
        firma="DM"
        content="really nice and tasty product for every day"
        price="0,04"
      />
      <MyCard
        name="Vegan Whey Pro"
        firma="bulk"
        content="for athlete sports persons"
        price="0,05"
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
  height: 100%;
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
  margin: 20px 0;
  color: #666;
  text-align: center;
}

ion-footer {
  text-align: center;
  padding: 10px 0;
  font-size: 0.9em;
  color: gray;
}
</style>
