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
    <ion-icon size="small" slot="end" name="add-circle" ></ion-icon>
  </ion-range>
</template>

<script lang="ts">
import { IonRange } from "@ionic/vue";
import { testing } from "googleapis/build/src/apis/testing";
import { defineComponent } from "vue";

export default defineComponent({
  components: { IonRange },
  methods: {
    onIonChange(event: { detail: any }) {
      console.log("ionChange emitted value:", typeof event.detail.value.upper);
      this.$emit("selectedPakgSize", event.detail)
    },
  },
});
</script>


<style>
  ion-range::part(tick) {
    background: #a2d2ff;
  }

  ion-range::part(tick-active) {
    background: #bde0fe;
  }

  ion-range::part(pin) {
    display: inline-flex;
    align-items: center;
    justify-content: center;

    background: #52E1F7;
    color: #000000;

    border-radius: 50%;
    transform: scale(1.01);

    top: -20px;

    min-width: 28px;
    height: 28px;
    transition: transform 120ms ease, background 120ms ease;
  }

  ion-range::part(pin)::before {
    content: none;
  }

  ion-range::part(knob) {
    background: #52E1F7;
  }

  ion-range::part(bar) {
    background: #52E1F7;
  }

  ion-range::part(bar-active) {
    background: #35c700;
  }
</style>