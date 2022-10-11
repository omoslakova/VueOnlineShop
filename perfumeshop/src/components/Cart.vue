<template>
<div>
    <CartItem
    v-for="(item) in cart"
    :key="item.id"
    :item="item"
    />
</div>
</template>

<script>
import CartItem from './CartItem.vue';

export default {
  name: "Cart",
  components: {
    CartItem,
  },
  props: {
        cart:{
        type: Object,
          required: true
            },
          },

  setup(props) {
    return {


    };
  },
};

</script>

<style scoped>

</style>