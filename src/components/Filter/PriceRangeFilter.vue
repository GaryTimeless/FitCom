<template>
  <ion-list>
    <ion-item>
      <ion-input
        :value="inputModel"
        @ionInput="onInput($event)"
        ref="ionInputEl"
        placeholder="Max Preis € "
      ></ion-input>
    </ion-item>
  </ion-list>
</template>

<script lang="ts">
import { IonInput, IonItem, IonList } from "@ionic/vue";
import { defineComponent, ref } from "vue";

export default defineComponent({
  components: { IonInput, IonItem, IonList },
  methods: {
    EmitValue(eventName: string, value: any) {
      console.log('Diese Methode wurde aufgerufen!');
      this.$emit(eventName, value);
    },
  },
  setup(_, context) {
    const ionInputEl = ref();
    const inputModel = ref("");
    const onInput = (ev) => {
      const selectMaxPrice = ev.target!.value;
      const filteredValue = 
        selectMaxPrice.replace(/[^0-9]+/g, "")

      console.log(filteredValue);
    context.emit("validMaxPrice", filteredValue);


        const inputCmp = ionInputEl.value;
        if (inputCmp !== undefined) {
          inputCmp.$el.value = filteredValue;
        }
        
    };

    return { ionInputEl, inputModel, onInput };
  },
});
</script>
