<template>
  <div class="container">
    <h1 class="my-4">ABC 團購網</h1>
    <div class="row">
      <div class="col-lg-8">
        <ProductList
          :products="products"
          :addToCart="addToCart"
          @ProductNumChange="handleProductNumChange"
        />
      </div>
      <div class="col-lg-4">
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
      { id: 1, name: "英日韓中翻譯筆【旗艦版】", pic_url: 'translate-pen.jpeg', owner: '滴妹', price: 100 },
      { id: 2, name: "AI 英文學習機", pic_url: 'english-learning-machine.jpeg', owner: '阿滴英文', price: 200 },
      { id: 3, name: "o'rest 歐瑞思側睡記憶枕", pic_url: '486-good-pillow.jpeg', owner: '豬豬隊友', price: 300 },
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