<template>
    <div>
      <h2>商品列表</h2>
      <div class="row">
        <div class="col-md-4" v-for="product in products" :key="product.id">
          <div class="card mb-4">
            <div class="card-body">
              <h5 class="card-title">{{ product.name }}</h5>
              <p class="card-text">{{ product.price }} 元</p>
              <button class="btn btn-primary" @click="addToCart(product)">加入購物車</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  // import { ref } from 'vue';
  
  export default {
    props: {
      products: Array,
      addToCart: Function,
    },
  };
  </script>