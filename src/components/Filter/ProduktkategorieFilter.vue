  <template>
    <ion-list>
      <ion-item>
        <ion-select
          v-model="selectedValues"
          aria-label="ProduktKategorie"
          placeholder="Wähle Produkt Kategorie aus"
          @ionChange="handleChange"
          :multiple="true"
        >
        <ion-select-option v-for="kategorie in productKategorie" :key="kategorie.value" :value="kategorie.value">
          {{ kategorie.label }}
        </ion-select-option>
        </ion-select>
      </ion-item>
    </ion-list>
  </template>



  <script lang="ts">
import { IonItem, IonList, IonSelect, IonSelectOption } from '@ionic/vue';
import { PropType, Ref, defineComponent, ref } from 'vue';


type ProduktKategorieType = {
  value: string;
  label: string;
};

export default defineComponent({
  components: { IonItem, IonList, IonSelect, IonSelectOption },
  props: {
    productKategorie: {
      type: Array as () => ProduktKategorieType[],
        required: true,
      },
      initialValue: {
      type: Object as PropType<ProduktKategorieType>,
      default: () => ({ value: '', label: '' }),
    },
    },
    data() {
      console.log("Initial Value:", this.initialValue); // Zeigt den initialen Wert in der Konsole an

      return {
        selectedValues: this.initialValue ? [this.initialValue.value] : [],
    };
  },
  methods: {
    handleChange(event: any) {
      // Hier werden die ausgewählten Firmen in der Konsole ausgegeben
      console.log('Ausgewählte ProduktKategorien:', event.detail.value);
      this.selectedValues = event.detail.value;
      this.$emit('SelectedProduktKategorieChange', this.selectedValues);
    },
    
    
  },
  });
  </script>
  
  <style>
    /* Ihre Styles */
  </style>
  