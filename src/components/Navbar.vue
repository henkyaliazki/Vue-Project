<template>
  <nav class="navbar navbar-light fixed-top">
    <div class="navbar-text ml-auto d-flex">
      <!-- membuat toggle UI slider status on-click -->
      <button class="btn btn-sm btn-outline-success" @click="$parent.$emit('toggle-slide')">
        <font-awesome-icon icon="dollar-sign"></font-awesome-icon>
      </button>
      <div class="dropdown ml-2" v-if="cart.length > 0">
        <!-- buat dropdown -->
        <button class="btn btn-sm btn-success dropdown-toggle" id="dropdownCart" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
          <span class="badge badge-pill badge-light">{{ cartQty }}</span>
          <font-awesome-icon icon="shopping-cart"></font-awesome-icon>
        </button>
        <price :value="Number(cartTotal)"> </price>
        <div class="dropdown-menu dropdown-menu-right" aria-labelledby="dropdownCart">
          <!-- isi dari dropdown -->
          <div v-for="(item, index) in cart" :key="index">
            <div class="dropdown-item-text text-nowrap text-right">
              <span class="badge badge-pill badge-warning align-text-top mr-1">
                {{ item.qty }}
              </span>
              {{ item.product.name }}
              <b>{{ (item.product.price * item.qty) | currencyFormat }} </b>
              <a href="#" class="badge badge-danger text-white" @click.stop="$parent.$emit('delete-item', index)">-</a>
            </div>
          </div>
          <router-link class="btn btn-sm btn-outline-info text-dark float-right mr-2" to="/checkout">Checkout</router-link>
        </div>
      </div>
    </div>
  </nav>
</template>

<script>
import Price from "./Price.vue";
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";

export default {
  name: "navbar",
  components: {
    Price,
    FontAwesomeIcon,
  },
  props: ["cart", "cartQty", "cartTotal"],
  filters: {
    currencyFormat: function (value) {
      return "Rp" + Number.parseFloat(value).toFixed(3);
    },
  },
};
</script>
