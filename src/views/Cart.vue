<script>
import axios from "axios";

export default {
  data: function () {
    return {
      cartedProducts: [],
    };
  },
  created: function () {
    this.showcartedProduct();
  },
  methods: {
    showcartedProduct: function () {
      console.log("hi");
      axios.get("http://localhost:3000/carted_products").then((response) => {
        console.log();
        console.log(response.data);
        this.cartedProducts = response.data;
      });
    },
    deleteCartedProduct: function (cartedProduct) {
      axios.delete("http://localhost:3000/carted_products/" + cartedProduct.id).then((response) => {
        console.log(response.data);
      });
    },
  },
};
</script>

<template>
  <div class="home">
    <div v-for="cartedProduct in cartedProducts" v-bind:key="cartedProduct.id">
      <div>Name:{{ cartedProduct.product.name }}</div>
      <div>Description: {{ cartedProduct.product.description }}</div>
      <div>Price: {{ cartedProduct.product.price }}</div>
      <div>Quantity: {{ cartedProduct.quantity }}</div>
      <div><img :src="cartedProduct.product.images[0].url" alt="haha" class="product-image" /></div>
      <button v-on:click="deleteCartedProduct(cartedProduct)">Delete</button>
      ---------------------------------
    </div>
    <button v-if="cartedProducts.length > 0">Order</button>
  </div>
</template>

<style>
.product-image {
  width: 100px;
}
</style>
