<script setup lang="ts">
import items from './assets/items.json';
import materials from './assets/materials.json';
import { computed, shallowRef } from 'vue';
import CustomSelect from './components/CustomSelect.vue';
import ProductCard from './components/ProductCard.vue';

const sortOptions = [
  { id: 0, name: 'Цена по возрастанию' },
  { id: 1, name: 'Цена по убыванию' },
];

const selectedSortId = shallowRef(0);
const selectedMaterialId = shallowRef(1);

const products = computed(() =>
  items
    .filter(
      (item) => Number(item.material) === Number(selectedMaterialId.value)
    )
    .sort((a, b) =>
      Number(selectedSortId.value) === 0
        ? a.price.current_price - b.price.current_price
        : b.price.current_price - a.price.current_price
    )
);
</script>

<template>
  <div class="container">
    <div class="header">
      <h2 class="header__title">Комплекты стеллажных систем</h2>
      <div class="header__filters">
        <CustomSelect
          v-model="selectedSortId"
          label="Сортировать по:"
          :options="sortOptions"
        />
        <CustomSelect
          v-model="selectedMaterialId"
          label="Материал"
          :options="materials"
        />
      </div>
    </div>
  </div>
  <div class="container">
    <div class="product-list">
      <ProductCard
        v-for="product in products"
        :key="product.id"
        :product="product"
      />
    </div>
  </div>
</template>

<style>
.container {
  display: flex;
  width: 1488px;
  flex-wrap: wrap;
  margin: auto;
}
.header {
  display: flex;
  flex-direction: column;
}
.header__filters {
  display: flex;
  gap: 24px;
}
.header__title {
  font-size: 36px;
  font-style: normal;
  font-weight: 600;
}
.product-list {
  display: grid;
  grid-template-columns: repeat(4, minmax(0, 1fr));
  row-gap: 48px;
  column-gap: 40px;
  margin: 41px 0;
}
</style>
