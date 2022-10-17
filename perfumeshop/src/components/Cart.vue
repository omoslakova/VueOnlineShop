<template>
  <dialog
      open
      class="cart-modal">
    <div class="cart-modal__items">
      <CartItem
          v-for="(item) in cart"
          :key="item.id"
          :item="item"
          @changeCartCount="emitChangeCartCount"
          @deleteFromCart="emitDeleteFromCart"
      />
    </div>
    <div class="cart-info">
      <p class="cart-info__total-price">
        Total: {{ cartTotalCost }} $
      </p>
      <p class="cart-info__total-positions">
        Positions: {{ cartTotalPositions }}
      </p>
      <button
          @click="emitToCloseCart"
          class="cart-info__btn-close"
      >
        CLOSE
      </button>
    </div>
  </dialog>
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
  emits: ['changeCartCount', 'deleteFromCart', 'toCloseCart'],

  setup(props, {emit}) {

    const emitChangeCartCount = () => {
      emit('changeCartCount')
    };

    const emitDeleteFromCart = (id) => {
      emit('deleteFromCart', id)
    };

    const emitToCloseCart = () => {
      emit('toCloseCart')
    };

    const cartTotalPositions = computed(() => {
      return Object.keys(props.cart).length;
    });

    const cartTotalCost = computed(() => {
      return Object.values(props.cart).reduce((sum, cartItem) => {
        const totalPricePerProduct = cartItem.count * cartItem.product.price
        return sum + totalPricePerProduct;
      }, 0)
    });

    return {
      emitChangeCartCount,
      emitDeleteFromCart,
      cartTotalCost,
      emitToCloseCart,
      cartTotalPositions
    };
  },
};

</script>

<style lang="scss" scoped>

.cart-modal {
  width: 900px;
  min-height: 600px;
  position: fixed;
  display: grid;
  grid-template-rows: 1fr auto;

  &__items {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(200px, 250px));
  }
}

.cart-info {
  display: grid;
  grid-template-columns: repeat(3, auto);
  justify-content: end;
  grid-gap: 40px;
  font-weight: bold;
  padding: 20px 20px 15px 100px;

  &__btn-close {
    background-color: white;
    color: black;
    border: 2px solid black;
    border-radius: 4px;
    width: 100px;
    height: 30px;
    font-weight: bold;
    margin-top: 10px;
  }
}


</style>