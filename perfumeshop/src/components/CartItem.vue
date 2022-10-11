<template>
<div>
  <p> Name: {{ item.product.title }} </p>
  <p> Description: {{ item.product.description }} </p>
  <p> Price: {{ item.product.price }} </p>
</div>
</template>

<script>
import {toRefs} from "@vue/reactivity";

export default {
  name: "CartItem",
  props: {
    item:{
      type: Object,
      required: true
    },
  },

  setup(props) {

    const {title, description, price} = toRefs(props.item)

    return {
      title,
      description,
      price
    };
  },
};

</script>

<style scoped>

</style>