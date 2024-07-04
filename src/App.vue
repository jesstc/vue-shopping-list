<template>
  <div class="container">
    <h1 class="my-4">Vue 3 商店</h1>
    <div class="row">
      <div class="col-md-8">
        <ProductList
          :products="products"
          :addToCart="addToCart"
          @ProductNumChange="handleProductNumChange"
        />
      </div>
      <div class="col-md-4">
        <ShoppingCart 
          :cart="cart"
          @RemoveId="removeFromCart"
          @CartNumChange="handleCartNumChange"
        />
      </div>
    </div>
  </div>
</template>

<script>
import { ref, reactive } from 'vue';
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

    const cart = reactive([]);
    const current_count = reactive([]);

    const addToCart = (product) => {
      const cartItem = cart.find(item => item.product.id === product.id);
      current_count[product.id] = current_count[product.id] ? current_count[product.id] : 1;

      if (cartItem) {
        cartItem.quantity += current_count[product.id];
      } else {
        cart.push({ product, quantity: current_count[product.id] });
      }
    };

    const removeFromCart = (productId) => {
      const index = cart.findIndex(item => item.product.id === productId);
      cart.splice(index, 1);
    };

    const handleProductNumChange = (updatedCount) => {
      current_count[updatedCount['id']] = updatedCount['newNum'];
    };

    const handleCartNumChange = (updatedCount) => {
      const updatedProduct = cart.find(item => item.product.id === updatedCount['id']);
      updatedProduct.quantity = updatedCount['newNum'];
    };

    return {
      products,
      cart,
      addToCart,
      removeFromCart,
      handleProductNumChange,
      handleCartNumChange,
    };
  }
};
</script>

<style>
/* 添加自定義樣式 */
</style>