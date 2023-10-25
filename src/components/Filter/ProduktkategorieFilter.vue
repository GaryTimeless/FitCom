<template>
    <ion-item>
      <ion-label>Produktkategorie</ion-label>
      <ion-select v-model="selectedKategorie">
        <ion-select-option v-for="kategorie in productKategorie" :key="kategorie.value" :value="kategorie.value">
          {{ kategorie.label }}
        </ion-select-option>
      </ion-select>
    </ion-item>
  </template>
  
  <script>
  export default {
    props: {
      productKategorie: {
        type: Array,
        required: true
      }
    },
    data() {
      return {
        selectedKategorie: null
      };
    }
  };
  </script>
  
  <style>
    /* Ihre Styles */
  </style>
  