<template>
  <!--eslint-disable-->
  <transition-group name="fade" tag="div" @beforeEnter="beforeEnter" @enter="enter" @leave="leave">
    <div
      class="row d-flex mb-3 align-items-center"
      v-for="(item, index) in products"
      :key="item.id"
      v-if="item.price<=Number(maximum)"
      :data-index="index"
    >
      <div class="col-1 m-auto">
        <button class="btn btn-info" @click="$parent.$emit('add', item)">+</button>
      </div>
      <div class="col-4">
        <img class="img-fluid d-block" :src="item.image" :alt="item.name">
      </div>
      <div class="col">
        <h3 class="text-info">{{ item.name }}</h3>
        <p class="mb-0">{{ item.description }}</p>
        <div class="h5 float-right" v-if="country==='India'">
          <price :prefix="'₹'" :conversion="83.75" :value="Number(item.price)"></price>
        </div>
        <div class="h5 float-right" v-if="country==='Usa'">
          <price :prefix="'$'" :conversion="1.03" :value="Number(item.price)"></price>
        </div>
        <div class="h5 float-right" v-if="country==='Europe'">
          <price :prefix="'€'" :conversion="0.87" :value="Number(item.price)"></price>
        </div>
      </div>
    </div>
  </transition-group>
</template>

<script>
import Price from "./Price.vue";

export default {
  name: "product-list",
  components: { Price },
  props: ["products", "maximum","country"],
  methods: {
    beforeEnter: function(el) {
      el.className = "d-none";
    },
    enter: function(el) {
      var delay = el.dataset.index * 100;
      setTimeout(function() {
        el.className =
          "row d-flex mb-3 align-items-center animated fadeInRight";
      }, delay);
    },
    leave: function(el) {
      var delay = el.dataset.index * 100;
      setTimeout(function() {
        el.className =
          "row d-flex mb-3 align-items-center animated fadeOutRight";
      }, delay);
    }
  }
};
</script>
