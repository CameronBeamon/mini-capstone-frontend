<script>
import axios from "axios";

export default {
  data: function () {
    return {
      products: [],
    };
  },
  created: function () {
    this.indexProducts();
  },
  methods: {
    indexProducts: function () {
      axios.get("http://localhost:3000/all_products").then((response) => {
        this.products = response.data;
      });
    },
  },
};
</script>

<template>
  <div class="home">
    <div v-for="product in products" v-bind:key="product.id">
      <div>
        {{ product.name }}
        <div><img :src="product.images[0].url" alt="Needs image" class="product-image" /></div>
        <router-link v-bind:to="`/product/${product.id}`">More details</router-link>
      </div>
    </div>
  </div>
</template>

<style>
.product-image {
  width: 100px;
}
</style>
