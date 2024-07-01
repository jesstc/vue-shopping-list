<template>
  <div class="container">
    <h1 class="my-4">Vue 3 商店</h1>
    <div class="row">
      <div class="col-md-8">
        <ProductList :products="products" :addToCart="addToCart" />
      </div>
      <div class="col-md-4">
        <ShoppingCart 
          :cart="cart"
          :increaseQuantity="increaseQuantity"
          :decreaseQuantity="decreaseQuantity"
          :removeFromCart="removeFromCart"
        />
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue';
import ProductList from './components/ProductList.vue';
import ShoppingCart from './components/ShoppingCart.vue';

export default {
  components: {
    ProductList,
    ShoppingCart,
  },
  setup() {
    const products = ref([
      { id: 1, name: '商品1', price: 100 },
      { id: 2, name: '商品2', price: 200 },
      { id: 3, name: '商品3', price: 300 },
    ]);

    const cart = ref([]);

    const addToCart = (product) => {
      const cartItem = cart.value.find(item => item.product.id === product.id);
      if (cartItem) {
        cartItem.quantity++;
      } else {
        cart.value.push({ product, quantity: 1 });
      }
    };

    const increaseQuantity = (item) => {
      item.quantity++;
    };

    const decreaseQuantity = (item) => {
      if (item.quantity > 1) {
        item.quantity--;
      } else {
        cart.value = cart.value.filter(i => i.product.id !== item.product.id);
      }
    };

    const removeFromCart = (productId) => {
      cart.value = cart.value.filter(item => item.product.id !== productId);
    };

    return {
      products,
      cart,
      addToCart,
      increaseQuantity,
      decreaseQuantity,
      removeFromCart,
    };
  }
};
</script>

<style>
/* 添加自定義樣式 */
</style>