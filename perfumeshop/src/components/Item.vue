<template>
  <div>
    <div>
      <p>
        {{ product.name }}
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
  name: "Item",
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