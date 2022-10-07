<template>
  <div>
    <Item
        v-for="(product) in products"
        :key="product.id"
        :product="product"
        @add="addProduct"
    />
  </div>
</template>

<script>

import Cart from './components/Cart.vue';
import Item from './components/Item.vue';
import { onMounted } from "@vue/runtime-core";
import axios from 'axios';
import {shallowRef} from "@vue/reactivity";

export default {
  name: "App",
  components: {
    Cart,
    Item,
  },
  setup() {
    let products = shallowRef([]);

      onMounted(() => {
          axios
          .get('https://dummyjson.com/products')
          .then(response => {
            products.value = response.data.products
            console.log(response)
          });
      })

        return {
          products,
        };
        },
      };

</script>


<style scoped>

</style>
