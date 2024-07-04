<template>
    <div>
      <h2>購物車</h2>
      <ul class="list-group">
        <li v-for="item in cart" :key="item.product.id" class="list-group-item d-flex justify-content-between align-items-center">
          <span class="me-auto align-self-center flex-grow-1">{{ item.product.name }}</span>
          <span class="align-self-center d-flex">
            <CounterBtn
              @ChangeNum="changeNum(item.product.id, $event)" 
              :productNum=item.quantity 
            />
            <span class="align-self-center">
              <button class="btn btn-md btn-danger" @click="removeId(item.product.id)">
                <i class="bi bi-trash"></i>
              </button>
            </span>
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
    },
    setup (props, { emit }) {

      const changeNum = (id, newNum) => {
        emit("CartNumChange", { id, newNum });
      }

      const removeId = (id) => {
        emit("RemoveId", id );
      }

      return {
        changeNum,
        removeId,
      }
    },
  });
  </script>