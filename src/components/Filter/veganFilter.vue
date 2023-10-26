<template>
    <ion-item>
      <ion-label>Vegan?</ion-label>
      <ion-checkbox v-model="isChecked" @ionChange="handleCheckboxChange"></ion-checkbox>
    </ion-item>
  </template>
  
  <script lang="ts">
  import { IonItem, IonLabel, IonCheckbox } from "@ionic/vue";
  import { defineComponent, ref, onMounted } from "vue";
  
  export default defineComponent({
    components: {
      IonItem,
      IonLabel,
      IonCheckbox,
    },
    props: {
      modelValue: Boolean,
    },
    setup(props, { emit }) {
      const isChecked = ref(props.modelValue);
  
      // Methode zur Aktualisierung des internen Werts und zum Emitten des Ereignisses
      const handleCheckboxChange = () => {
        isChecked.value = !isChecked.value;
        // Emitiere den Wert an die übergeordnete Komponente
        console.log("test")
        emit("update:modelValue", isChecked.value);
      };
  
      return {
        isChecked,
        handleCheckboxChange,
      };
    },
  });
  </script>
  
  
  
  
   <!-- <ion-checkbox  slot="start" v-model="isChecked">Vegan?</ion-checkbox> -->