<template>
  <div>
    <CartItem
        v-for="(item) in cart"
        :key="item.id"
        :item="item"
    />
    <p
        v-if="Object.keys(cart).length"
    >
      Total: {{ cartTotalCost }}
    </p>
  </div>
</template>

<script>
import CartItem from './CartItem.vue';
import {computed} from "@vue/reactivity";

export default {
  name: "Cart",
  components: {
    CartItem,
  },
  props: {
    cart: {
      type: Object,
      required: true
    },
  },
  emits: ['changeCartCount', 'deleteFromCart'],

  setup(props, {emit}) {

    const emitChangeCartCount = () => {
      emit('changeCartCount')
    };

    const emitDeleteFromCart = (index) => {
      emit('deleteFromCart', index)
    };

    const cartTotalCost = computed(() => {
        return Object.values(props.cart).reduce((sum, cartItem) => {
          const totalPricePerProduct = cartItem.count * cartItem.product.price
          console.log(totalPricePerProduct)
            return sum + totalPricePerProduct;
          }, 0)
        });

    return {
      emitChangeCartCount,
      emitDeleteFromCart,
      cartTotalCost
        };
      },
    };

</script>

<style scoped>

</style>