<template>
    <div>
      <h2>購物車</h2>
      <ul class="list-group">
        <li v-for="item in cart" :key="item.product.id" class="list-group-item d-flex justify-content-between align-items-center">
          <span class="me-auto p-2 align-self-center">{{ item.product.name }}</span>
          <span class="p-2 align-self-center">
            <span class="input-group mb-3">
              <button class="btn btn-sm btn-secondary" @click="decreaseQuantity(item)">-</button>
              <span class="input-group-text">{{ item.quantity }}</span>
              <button class="btn btn-sm btn-secondary" @click="increaseQuantity(item)">+</button>
            </span>
          </span>
          <span class="p-2 align-self-center">
            <button class="btn btn-sm btn-danger" @click="removeFromCart(item.product.id)">
              <i class="bi bi-trash"></i>
            </button>
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