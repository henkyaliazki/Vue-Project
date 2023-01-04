<template>
  <transition-group name="fade" tag="div" @before-enter="before" @enter="enter" @leave="leave">
    <div class="row d-none mb-3 align-items-center" v-for="(item, index) in showItem" :key="item.id" :data-index="index">
      <!-- ini adalah pengkondisian dalam vue -->
      <div class="col-1 m-auto">
        <!-- event pada vue, jadi jika kita click tombol + maka item akan masuk(push) ke cart -->
        <button class="btn btn-info" @click="$emit('add', item)">+</button>
      </div>
      <div class="col-sm-4">
        <!-- binding elemet/atribut dengan cara menggunakan tanda : jadi untuk memanggil data tidak perlu dengan {{}} tapi lebih mudah dengan tanda : diawal -->
        <img :src="item.image" :alt="item.title" class="img-fluid d-block" />
      </div>
      <div class="col">
        <!-- ini reaktive data  -->
        <h2 class="text-info">{{ item.name }}</h2>
        <p class="mb-0">{{ item.description }}</p>
        <!-- cara menggunakan filters dengan symbol |  di ikuti dengan nama filtersnya -->
        <div class="h5 float-right">
          <price :value="Number(item.price)"></price>
        </div>
      </div>
    </div>
  </transition-group>
</template>
<script>
import Price from "./Price.vue";

export default {
  name: "product-list",
  components: {
    Price,
  },
  props: ["products", "maximum"],
  computed: {
    showItem: function () {
      let max = this.maximum;
      return this.products.filter(function (item) {
        return item.price <= max;
      });
    },
  },
  methods: {
    before: function (el) {
      el.className = "d-flex";
    },
    enter: function (el) {
      let delay = el.dataset.index * 100;
      setTimeout(function () {
        el.className = "row d-flex mb-3 align-items-center animated fadeInRight";
      }, delay);
    },
    leave: function (el) {
      let delay = el.dataset.index * 100;
      setTimeout(function () {
        el.className = "row d-flex mb-3 align-items-center animated fadeOutRight";
      }, delay);
    },
  },
};
</script>
