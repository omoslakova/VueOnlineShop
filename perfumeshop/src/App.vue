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

export default {
  name: "App",
  components: {
    Cart,
    Item,
  },
  setup() {
    const products = [
      {
        id: 1,
        name: 'Lancome',
        image: 'https://vanille.by/assets/images/products/65048/large/lancome-la-vie-est-belle-2.jpg',
        price: 250,
      },
      {
        id: 2,
        name: 'Bulgari',
        image: 'https://allparfume.by/images/parfumes/bulgari_omnia_amethyste.jpg',
        price: 250,
      },
      {
        id: 3,
        name: 'Lancome',
        image: 'https://vanille.by/assets/images/products/65048/large/lancome-la-vie-est-belle-2.jpg',
        price: 250,
      }
    ];



    return {
      products,
   
    };
  },
};

</script>


<style scoped>

</style>
