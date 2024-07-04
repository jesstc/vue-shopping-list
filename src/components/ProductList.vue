<template>
    <div>
      <h2>商品列表</h2>
      <div class="row">
        <div class="col-md-4" v-for="(product, index) in products" :key="product.id">
          <div class="card mb-4">
            <img src="../assets/logo.png" class="card-img-top" alt="...">
            <div class="card-body">
              <h5 class="card-title">{{ product.name }}</h5>
              <p class="card-text">
                團購主： {{ product.owner }}
                <br><br>
                <span class="badge text-bg-danger">團購價：${{ product.price }} </span>
                <CounterBtn @ChangeNum="changeNum" :productNum=initial_counts[index] />
              </p>
              <button class="btn btn-primary" @click="addToCart(product)">
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
  import { toRefs, defineComponent, reactive, watch } from 'vue';
  
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
      const initial_counts = reactive(new Array(products.value.length).fill(0));

      const changeNum = (newNum) => {
        initial_counts.values = newNum;
        emit("ProductNumChange", newNum)
      }

      watch(initial_counts, (newVal) => {
        initial_counts.values = newVal;
      });

      return {
        initial_counts,
        changeNum,
      }
    },
  });

  </script>