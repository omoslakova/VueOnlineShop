<template>
  <div>
    <p>
      Name: {{ product.title }}
    </p>
    <p>
      Description: {{ product.description }}
    </p>
    <p>
      Price: {{ product.price }}
    </p>
    <p>
      Quantity:
    </p>

    <span>
        <span
            @click="changeCartCount(-1)"
        >
        -
        </span>
           {{ count }}
        <span
            @click="changeCartCount(1)"
        >
        +
        </span>
      </span>
    <button
        @click=""
    >
      DELETE
    </button>
  </div>
</template>

<script>
import {toRefs, watch} from 'vue';

export default {
  name: "CartItem",
  props: {
    item: {
      type: Object,
      required: true
    },
    index: {
      type: Number,
      required: true
    },
  },
  emits: ['changeCartCount', 'deleteFromCart'],
  setup(props, {emit}) {

    const {product, count} = toRefs(props.item);

    const emitChangeCartCount = () => {
        emit('changeCartCount')
    }

    watch(
        () => count.value,
        (newCountValue) => {
        console.log('watch count', newCountValue);
        if (newCountValue === 0) {
        emit('deleteFromCart');
        }
    });

    const changeCartCount = (value) => {
      count.value += value;
    }

    return {
      product,
      count,
      changeCartCount,
      emitChangeCartCount,
    };
  },
};
</script>

<style scoped>

</style>