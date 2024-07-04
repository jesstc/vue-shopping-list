<template>
    <div>
      <h2>購物車</h2>
      <ul class="list-group">
        <li v-for="item in cart" :key="item.product.id" class="list-group-item d-flex justify-content-between align-items-center">
          <span class="me-auto p-2 align-self-center">{{ item.product.name }}</span>
          <CounterBtn 
            @ChangeNum="changeNum(item.product.id, $event)" 
            :productNum=item.quantity 
          />
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
  import CounterBtn from './CounterBtn.vue';
  import { defineComponent } from 'vue';
  
  export default defineComponent({
    components: {
      CounterBtn,
    },
    props: {
      cart: Array,
      removeFromCart: Function,
    },
    setup (props, { emit }) {

      const changeNum = (id, newNum) => {
        emit("CartNumChange", { id, newNum })
      }

      return {
        changeNum,
      }
    },
  });
  </script>