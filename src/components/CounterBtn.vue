<template>
    <div class="p-2 align-self-center">
        <span class="input-group mb-3">
            <button class="btn btn-sm btn-secondary" @click="increaseQuantity(item)">-</button>
            <span class="input-group-text">{{ item.quantity }}</span>
            <button class="btn btn-sm btn-secondary" @click="increaseQuantity(item)">+</button>
        </span>
    </div>
</template>

<script>
  
export default {
    props: {
        item: Object,
        increaseQuantity: Function,
        decreaseQuantity: Function,
    },
};

</script>