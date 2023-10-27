<template>
  <ion-label
    style="padding: 0 0 5% 0; width: 150px; font-size: 20px"
    position="stacked"
    >Pkg (g)</ion-label
  >
  <ion-range
    aria-label="Dual Knobs Range"
    :dual-knobs="true"
    :ticks="true"
    :snaps="true"
    :pin="true"
    :step="500"
    :min="500"
    :max="5000"
    :value="{ lower: 500, upper: 1000 }"
    @ionChange="onIonChange"
  >
    <ion-icon size="small" slot="start" name="remove-circle"></ion-icon>
    <ion-icon size="small" slot="end" name="add-circle"></ion-icon>
  </ion-range>
</template>

<script lang="ts">
import { IonRange } from "@ionic/vue";
import { testing } from "googleapis/build/src/apis/testing";
import { defineComponent } from "vue";

export default defineComponent({
  components: { IonRange },
  methods: {
    onIonChange({ detail}) {
      console.log("ionChange emitted value:", detail.value);
      this.$emit("selectedPakgSize", detail)
    },
  },
});
</script>
