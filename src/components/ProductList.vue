<template>
    <div>
      <h2>商品列表</h2>
      <div class="row">
        <div class="col-md-4" v-for="(product, index) in products" :key="product.id">
          <div class="card mb-4">
            <img :src="imagePath(product.pic_url)" @error=handleImageError class="card-img-top" alt="...">
            <div class="card-body">
              <h5 class="card-title">{{ product.name }}</h5>
              <p class="card-text">
                團購主： {{ product.owner }}
              </p>
              <span class="d-flex justify-content-between align-items-center">
                <span class="badge text-bg-danger">團購價：${{ product.price }} </span>
                <CounterBtn @ChangeNum="changeNum(product.id, $event)" :productNum=initial_counts[index] />
              </span>
              <button class="btn btn-primary text-nowrap w-100" @click="addToCart(product, initial_counts[index])">
                <i class="bi bi-cart"></i> 加入購物車
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script>

  import CounterBtn from './CounterBtn.vue';
  import { toRefs, defineComponent, reactive } from 'vue';
  
  export default defineComponent({
    components: {
      CounterBtn,
    },
    props: {
      products: Array,
      addToCart: Function, 
    },
    setup (props, { emit }) {
      const { products } = toRefs(props);
      const initial_counts = reactive(new Array(products.value.length).fill(1));

      const imagePath = (path) => {
        try {
          return require(`@/assets/${path}`);
        } catch {
          return path;
        }
      };

      const handleImageError = (event) => {
        event.target.src = require('@/assets/logo.png');
      };

      const changeNum = (id, newNum) => {
        initial_counts.values = newNum;
        emit("ProductNumChange", { id, newNum});
      }

      return {
        imagePath,
        handleImageError,
        initial_counts,
        changeNum,
      }
    },
  });

  </script>