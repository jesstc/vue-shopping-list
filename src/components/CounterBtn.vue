<template>
    <div class="p-2 align-self-center">
        <span class="input-group mb-3">
            <button class="btn btn-sm btn-secondary" @click="changeQantity(-1)">-</button>
            <span class="input-group-text">{{ localProductNum }}</span>
            <button class="btn btn-sm btn-secondary" @click="changeQantity(1)">+</button>
        </span>
    </div>
</template>

<script>
import { defineComponent, toRefs, ref, watch } from 'vue';
  
export default defineComponent({
    props: {
        productNum: Number,
    },
    setup(props, { emit }) {
        const { productNum } = toRefs(props);
        const localProductNum = ref(productNum.value);

        const changeQantity = (increase_decrease) => {
            (localProductNum.value > 1 || increase_decrease > 0) && 
                (localProductNum.value += increase_decrease);
            emit("ChangeNum", localProductNum.value);
        };

        watch(productNum, (newVal) => {
            localProductNum.value = newVal;
        });

        return {
            localProductNum,
            changeQantity,
        }
    }
});

</script>