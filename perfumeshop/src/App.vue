<template>
  <div>
    <p
        v-if="Object.keys(cart).length"
    >
        Cart
    </p>
  <Cart
      v-if="Object.keys(cart).length"
      :key="cart.id"
      :cart="cart"
      @changeCartCount="changeCartCount"
  />
</div>
  <div>
    <Product
        v-for="(product) in products"
        :key="product.id"
        :product="product"
        @addProduct="addProduct"
    />
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
  setup() {
    const products = shallowRef([]);

    const cart = ref({})

    const addProduct = (product) => {
      cart.value[product.id] = {
        product,
        count: 1
      };
    };


    const removeFromCart = (index) => {
      delete cart.value
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

            };
      },
    };

</script>


<style scoped>

</style>
