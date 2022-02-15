<script>
import axios from "axios";

export default {
  data: function () {
    return {
      product: [],
      productParams: {},
      quantity: 0,
    };
  },
  created: function () {
    this.showProduct();
  },
  methods: {
    showProduct: function () {
      axios.get("http://localhost:3000/all_products/" + this.$route.params.id).then((response) => {
        this.product = response.data;
      });
    },
    addToCart: function () {
      this.productParams.quantity = this.quantity;
      this.productParams.product_id = this.$route.params.id;
      console.log(this.productParams);
      axios.post("http://localhost:3000/carted_products/", this.productParams).then((response) => {
        console.log(response.data);
      });
    },
  },
};
</script>

<template>
  <div class="home">
    <div>{{ product.name }}</div>
    <div>{{ product.description }}</div>
    <div>{{ product.price }}</div>
    <div><img :src="product.images[0].url" alt="haha" class="product-image" /></div>
    <input type="number" name="quantity" v-model="quantity" />
    <button v-on:click="addToCart()">Add to cart</button>
  </div>
</template>

<style>
.product-image {
  width: 100px;
}
</style>
