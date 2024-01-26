<template>
  <div>
    <ion-list v-if="products && products.length > 0">
      <ion-item-group v-for="product in products" :key="product.id"> 
        <ion-item>
          <div class="label-wrapper">
            <ion-label class="table-cell">{{ product.firma }}</ion-label>
            <ion-label class="table-cell">{{ product.produktkategorie }}</ion-label>
            <ion-label class="table-cell">{{ product.name }}</ion-label>
            <ion-label class="table-cell">{{ product.preisPerPackung }} €</ion-label>
            <ion-label class="table-cell">{{ product.preisPerKG }} €</ion-label>
            <ion-label class="table-cell">{{ product.portionenPerPkg }}</ion-label>
            <ion-label class="table-cell">{{ product.gewichtPerPkg }} g</ion-label>
            <ion-label class="table-cell">{{ product.vegan }}</ion-label>
          </div>
        </ion-item>
      </ion-item-group>
    </ion-list>
  </div>
</template>


<script setup lang="ts">
import { IonItem, IonLabel, IonList, IonItemGroup } from "@ionic/vue";
interface Product {
  id: number;
  firma: string;
  produktkategorie: string;
  name: string;
  preisPerPackung: string;
  preisPerKG: string;
  portionierung: string;
  portionenPerPkg: string;
  gewichtPerPkg: string;
  vegan: string;
}

const props = defineProps({
  products: {
    type: Array as () => Product[],
    required: true
  }
});

</script>


<style scoped>
.table-cell {
  padding: 10px;
  min-width: 200px;
  text-align: center;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.label-wrapper {
  display: flex;
  overflow-x: auto;
}

/* Anpassung für Light und Dark Mode */
.table-cell {
  background-color: #ffffff;
  color: #000000;
}

@media (prefers-color-scheme: dark) {
  .table-cell {
    background-color: rgb(48, 48, 24);
    color: #ffffff;
  }
}
</style>
