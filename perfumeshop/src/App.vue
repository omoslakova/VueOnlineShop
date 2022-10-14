<template>
  <div class="wrapper">
    <div class="cart">
      <button
        @click="changeIsCartOpen(true)"
        class="cart__btn-open"
      >
        Open cart
      </button>

      <Cart
        v-if="isCartOpen"
        :key="cart.id"
        :cart="cart"
        @deleteFromCart="removeFromCart"
        @toCloseCart="changeIsCartOpen(false)"
      />
    </div>

  <div class="product">
    <Product
        v-for="(product) in products"
        :key="product.id"
        :product="product"
        @addProduct="addProduct"
    />
  </div>
  </div>
</template>

<script>

import Cart from './components/Cart.vue';
import Product from './components/Product.vue';
import {onMounted, shallowRef} from "@vue/runtime-core";
import axios from 'axios';
import {ref} from "@vue/reactivity";

export default {
  name: "App",
  components: {
    Cart,
    Product,
  },
  emits: ['deleteProduct'],
  setup() {

    const totalArticles = ref()
    const products = shallowRef([]);

    const cart = ref({})

    const isCartOpen = ref(false);

    const addProduct = (product) => {
      cart.value[product.id] = {
        product,
        count: 1
      };
    };

    const changeIsCartOpen = (newValue) => {
      isCartOpen.value = newValue
    }

    const removeFromCart = (id) => {
      delete cart.value[id]
    }

    onMounted(() => {
      axios
          .get('https://dummyjson.com/products')
          .then(response => {
            products.value = response.data.products
          });
    })

    return {
      products,
      cart,
      addProduct,
      removeFromCart,
      isCartOpen,
      changeIsCartOpen,
      totalArticles
    };
    },
  };

</script>

<style lang="scss" scoped>

.wrapper {
  font-weight: normal;
  color: darkslategray;
}

.cart {
  margin: 15px 0;
  &__btn-open {
    background-color: white;
    color: black;
    border: 2px solid black;
    border-radius: 4px;
    width: 100px;
    height: 30px;
    font-weight: bold;
  }
}

.product {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(400px, 1fr));
  grid-gap: 40px;
}

</style>
