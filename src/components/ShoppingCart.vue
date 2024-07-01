<template>
    <div>
      <h2>購物車</h2>
      <ul class="list-group">
        <li v-for="item in cart" :key="item.product.id" class="list-group-item d-flex justify-content-between align-items-center">
          <span>{{ item.product.name }} x {{ item.quantity }}</span>
          <span>
            <button class="btn btn-sm btn-secondary" @click="decreaseQuantity(item)">-</button>
            <button class="btn btn-sm btn-secondary" @click="increaseQuantity(item)">+</button>
            <button class="btn btn-sm btn-danger" @click="removeFromCart(item.product.id)">移除</button>
          </span>
        </li>
      </ul>
    </div>
  </template>
  
  <script>
  // import { ref } from 'vue';
  
  export default {
    props: {
      cart: Array,
      increaseQuantity: Function,
      decreaseQuantity: Function,
      removeFromCart: Function,
    },
  };
  </script>