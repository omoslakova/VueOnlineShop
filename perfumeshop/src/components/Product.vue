<template>
  <div class="product-item">
    <img
        :src="product.images[0]"
        :alt="product.title"
        class="product-item__img"
    >
    <div class="product-info">
      <p class="product-info__product-title">
        {{ product.title }}
      </p>
    <p>
      {{ product.description }}
    </p>
      <p class="product-info__product-price">
          Price: {{ product.price }} $
      </p>
      <div>
      <button
          class="product-info__btn-add"
          @click="emitAddProduct"
      >
        Add to cart
      </button>
      </div>
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

<style lang="scss" scoped>

.product-item {
  text-align: center;
  border-radius: 6px;
  padding: 20px 30px;
  box-shadow: 0 0 8px 0 #e0e0e0;
  display: flex;
    &__img {
    width: 400px;
    height: 300px;
    }
    &:hover {
      box-shadow: 0 0 8px 0 teal;
    }
}
.product-info {
  display: grid;
  grid-template-rows: repeat(4, 1fr);
  padding: 10px;
    &__product-title {
      font-weight: bold;
      font-size: 20px;
    }
    &__product-price {
      font-weight: bolder;
      color: teal;
    }
    &__btn-add {
      background-color: white;
      color: black;
      border: 2px solid #e0e0e0;
      border-radius: 4px;
      width: 100px;
      height: 30px;
      font-weight: bold;
      box-shadow: 0 0 4px 0 #e0e0e0;
      &:hover {
        box-shadow: 0 0 4px 0 teal;
      }
    }
}

</style>