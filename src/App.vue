<template>
  <div id="app" class="container mt-5">
    <h1>Tokopadia</h1>
    <product-list :products="products" :maximum="maximum"> </product-list>
  </div>
</template>

<script>
// import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
// import Price from "./components/Price.vue";
import ProductList from "./components/ProductList.vue";

export default {
  name: "app",
  data: function () {
    return {
      maximum: 50,
      products: [],
    };
  },
  components: {
    // FontAwesomeIcon,
    // Price,
    ProductList,
  },
  mounted: function () {
    fetch("https://api.storerestapi.com/products")
      .then((response) => response.json())
      .then((data) => {
        this.products = data;
        console.log(data);
      });
  },
};
</script>
