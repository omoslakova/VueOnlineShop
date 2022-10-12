<template>
  <div>
    <div>
      <p>
        {{ product.title }}
      </p>
      <p>
        Price: {{ product.price }} р.
      </p>
      <button
          @click="emitAddProduct"
      >
        ADD
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Product",
  props: {
    product: {
      type: Object,
      required: true,
    },
  },
  emits: ['addProduct'],

  setup(props, {emit}) {

    const emitAddProduct = () => {
      emit('addProduct', props.product);
    }
    return {
      emitAddProduct
    };
  },
};

</script>

<style scoped>

</style>