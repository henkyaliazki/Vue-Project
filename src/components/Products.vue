<template>
  <div>
    <h1>TokoGadai</h1>
    <navbar :cart="cart" :cartQty="cartQty" :cartTotal="cartTotal" @toggle-slide="toggleSlider" @delete-item="deleteItem"></navbar>
    <price-slider :sliderStatus="sliderStatus" :maximum.sync="maximum"></price-slider>
    <pre></pre>
    <product-list :products="products" :maximum="maximum" @add-item="addItem"></product-list>
  </div>
</template>

<script>
import Navbar from "./Navbar.vue";
import ProductList from "./ProductList.vue";
import PriceSlider from "./PriceSlider.vue";

export default {
  name: "products",
  props: ["maximum", "products", "cart", "cartQty", "cartTotal", "sliderStatus", "sliderState"],
  components: {
    Navbar,
    ProductList,
    PriceSlider,
  },
  methods: {
    toggleSlider: function () {
      this.$emit("toggle");
    },
    addItem: function (item) {
      this.$emit("add", item);
    },
    deleteItem: function (index) {
      this.$emit("delete", index);
    },
  },
};
</script>
