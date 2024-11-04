<template>
    <ion-page>
      <ion-header>
        <ion-toolbar>
          <ion-title>Welcome to FitCom</ion-title>
        </ion-toolbar>
      </ion-header>
  
      <ion-content class="ion-padding">
        <div class="hero-section">
          <ion-img src="path/to/your/image.jpg" alt="Hero Image"></ion-img>
          <h2>Your Fitness Journey Starts Here</h2>
        </div>
  
        <ion-button expand="block" @click="navigateToDetails">
          See Top 10 Protein Powders
        </ion-button>
  
        <ion-list>
          <ion-item>
            <ion-label>Feature 1</ion-label>
          </ion-item>
          <ion-item>
            <ion-label>Feature 2</ion-label>
          </ion-item>
          <ion-item>
            <ion-label>Feature 3</ion-label>
          </ion-item>
        </ion-list>
  
        <ion-footer>
          <p>&copy; 2024 FitCom. All rights reserved.</p>
        </ion-footer>
      </ion-content>
    </ion-page>
  </template>
  
  <script lang="ts">
  import { defineComponent, ref } from 'vue';
  
  export default defineComponent({
    setup() {
      const message = ref("Hello World");
  
      function showMessage() {
        console.log(message.value);
      }
  
      return {
        message,
        showMessage,
      };
    },
  });
  </script>
  
  <style scoped>
  .hero-section {
    text-align: center;
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