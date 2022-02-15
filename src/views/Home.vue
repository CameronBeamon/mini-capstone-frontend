<script>
import axios from "axios";

export default {
  data: function () {
    return {
      products: [],
      search: "",
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
    filterProducts: function () {
      return this.products.filter((product) => {
        var lowerProduct = product.name.toLowerCase();
        var lowerSearch = this.search.toLowerCase();
        return lowerProduct.includes(lowerSearch);
      });
    },
  },
};
</script>

<template>
  <div class="home">
    <div class="search-bar">
      Search by name:
      <input v-model="search" type="text" />
    </div>

    <div v-for="product in filterProducts()" v-bind:key="product.id">
      <div class="Products">
        {{ product.name }}
        <div><img :src="product.images[0].url" alt="Needs image" class="product-image" /></div>
        <router-link v-bind:to="`/product/${product.id}`">More details</router-link>
      </div>
    </div>
  </div>
</template>

<style>
.Products {
  text-align: center;
}
.product-image {
  width: 100px;
}
.search-bar {
  text-align: right;
}
</style>
