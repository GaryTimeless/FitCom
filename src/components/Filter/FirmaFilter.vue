<template>
  <ion-list>
    <ion-item>
      <ion-select
        aria-label="Firma"
        placeholder="Wähle Firmen aus"
        :compareWith="compareWith"
        @ionChange="handleChange"
        :multiple="true"
      >
        <ion-select-option v-for="firma in firmen" :value="firma.value">{{
          firma.label
        }}</ion-select-option>
      </ion-select>
    </ion-item>
  </ion-list>
</template>

<!-- Alternaitve -->
<!-- <script lang="ts">
DAS IST DER VERSUCH ES AN DIE ANDEREN KOMPONENTEN ANZUPASSEN - Die haben nämlich kein export default defineComponent({

import { IonItem, IonList, IonSelect, IonSelectOption } from "@ionic/vue";
import { Ref, defineComponent, ref } from "vue";

defineProps({
  firmen: {
    type: Array,
    required: true,
  },
});
const emit = defineEmits();
const selectedValues = ref<string[]>([]);
const compareWith = (o1: any, o2: any) => {
  if (!o1 || !o2) {
    return o1 === o2;
  }

  if (Array.isArray(o2)) {
    return o2.some((o) => o.value === o1.value);
  }

  return o1.value === o2.value;
};
const handleChange = (event: any) => {
      // Hier werden die ausgewählten Firmen in der Konsole ausgegeben
      console.log('Ausgewählte Firmen:', event.detail.value);
      selectedValues.value = event.detail.value;
      emit('SelectedFirmaChange',selectedValues);
    }


</script> -->

<!-- Übergabe der Daten - Anzeige Kaputt -->
<!-- <script lang="ts">

  Hiermit funktioniert der Code insofern man die ausgewählten Firmen an eine andere komponente (eltern) übergibt
  Aber die Komponente an siche spinnt. 
  Man wählt X1 und X2 und es steht in der Website X1, X1 da



import { IonItem, IonList, IonSelect, IonSelectOption } from '@ionic/vue';
import { Ref, defineComponent, ref } from 'vue';
//TODO seltsam, das hier ein export default ist und so. Oben ein Versuch, das zu umgehen. Klappt nicht. 
export default defineComponent({
  components: { IonItem, IonList, IonSelect, IonSelectOption },
  props: {
    firmen: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      // selectedValues: [] as string[], // Hier wird ein leeres Array für die ausgewählten Werte initialisiert
    };
  },
  methods: {
    compareWith(o1: any, o2: any) {
      if (!o1 || !o2) {
        return o1 === o2;
      }

      if (Array.isArray(o2)) {
        return o2.some((o) => o.value === o1.value);
      }

      return o1.value === o2.value;
    },
    handleChange(event: any) {
      // Hier werden die ausgewählten Firmen in der Konsole ausgegeben
      console.log('Ausgewählte Firmen:', event.detail.value);
      this.selectedValues = event.detail.value;
      this.$emit('SelectedFirmaChange', this.selectedValues);
    },
  },
});
</script> -->

<!-- Anzeige Oke, keine Übergabe -->
<script lang="ts">

// Hier funktioniert NUR die Componente - aber die Daten werden nicht weiter gegeben


import { IonItem, IonList, IonSelect, IonSelectOption } from '@ionic/vue';
import { Ref, defineComponent, ref } from 'vue';
//TODO seltsam, das hier ein export default ist und so. Oben ein Versuch, das zu umgehen. Klappt nicht. 
export default defineComponent({
  components: { IonItem, IonList, IonSelect, IonSelectOption },
  props: {
    firmen: {
      type: Array,
      required: true,
    },
  },
  data() {
    
  },
  methods: {
    
  },
});
</script>
