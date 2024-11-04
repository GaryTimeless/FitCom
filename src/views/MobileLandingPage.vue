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
        </div>
  
        <ion-button expand="block" @click="navigateToDetails">
          See Top 10 Protein Powders
        </ion-button>
  
        <MyCard
          title="Protein Shake"
          subtitle="Best Seller"
          content="High quality whey protein for your muscles."
          imageSrc="src/img/ProteinExample.jpg"
        />
  
        <ion-footer>
          <p>&copy; 2024 FitCom. All rights reserved.</p>
        </ion-footer>
      </ion-content>
    </ion-page>
  </template>
  
  <script setup lang="ts">
  import { ref } from 'vue';
  import MyCard from '@/components/MyCard.vue';
  
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
  
  ion-footer {
    text-align: center;
    padding: 10px 0;
    font-size: 0.9em;
    color: gray;
  }
  </style>