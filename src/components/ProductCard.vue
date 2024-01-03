<script setup lang="ts">
import { Product } from '../types/Product';

interface Props {
  product: Product;
}
const { product } = defineProps<Props>();

const addToCart = (product: Product) => {
  let productCart = JSON.parse(localStorage.getItem('productCart') as string) || [];
  productCart.push(product);
  localStorage.setItem('productCart', JSON.stringify(productCart));
};

const addToFavorites = (product: Product) => {
  let favorites = JSON.parse(localStorage.getItem('favorites') as string) || [];
  favorites.push(product);
  localStorage.setItem('favorites', JSON.stringify(favorites));
};
</script>

<template>
  <div class="card">
    <div
      v-show="product.price.old_price"
      class="card__discount"
    >
      Cкидка
    </div>
    <img
      :src="product.image.url"
      alt="img"
    />
    <div class="card__info info-block">
      <span class="info-block__code">{{ product.code }}</span>
      <span class="info-block__name">{{ product.name }}</span>
      <div class="info-block__footer footer">
        <div class="footer__price price">
          <span
            v-show="product.price.old_price"
            class="price__old"
            >{{ product.price.old_price }}₽</span
          >
          <span>{{ product.price.current_price }}₽</span>
        </div>
        <div class="footer__buttons">
          <button @click="addToCart(product)">
            <img src="../assets/svg/shopping-cart.svg" />
          </button>
          <button @click="addToFavorites(product)">
            <img src="../assets/svg/basic-heart.svg" />
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
button {
  border: none;
}
.card {
  width: 336px;
  height: 352px;
  flex-shrink: 0;
  border: 1px solid #eee;
  padding: 9px 12px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
  position: relative;
}
.card__info {
  display: flex;
  flex-direction: column;
  width: 100%;
}
.info-block__code {
  color: #888;
  font-size: 10px;
  font-style: normal;
  font-weight: 400;
  line-height: 140%;
  letter-spacing: 0.2px;
  margin-bottom: 6px;
}
.info-block__name {
  font-size: 16px;
  font-style: normal;
  font-weight: 500;
  line-height: 140%;
  letter-spacing: 0.32px;
  font-weight: 500;
  margin-bottom: 9px;
}
.info-block__footer {
  display: flex;
  justify-content: space-between;
}
.footer__price {
  display: flex;
  gap: 9px;
  font-size: 16px;
  font-style: normal;
  font-weight: 400;
  line-height: 140%;
  letter-spacing: 0.32px;
}
.price__old {
  color: #888;
  text-decoration: line-through;
}
.footer__buttons {
  display: flex;
  gap: 11px;
  justify-items: center;
  justify-content: space-between;
}
.card__discount {
  position: absolute;
  top: 8px;
  left: 0px;
  background-color: #eb5757;
  color: #fff;
  padding: 3px 16px;
  font-size: 14px;
  font-style: normal;
  font-weight: 500;
  line-height: 130%; /* 18.2px */
  letter-spacing: 0.14px;
}
</style>
