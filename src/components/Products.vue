<template>
  <div>
    <h1>My Shop</h1>
    <navbar :cart="cart" :cartQty="cartQty" :cartTotal="cartTotal" ></navbar>
    <price-slider :sliderStatus="sliderStatus" :maximum.sync="maximum"></price-slider>
    <product-list :country="country" :maximum="maximum" :products="products" ></product-list>
  </div>
</template>
<script>
import Navbar from "./Navbar.vue";
import PriceSlider from "./PriceSlider.vue";
import ProductList from "./ProductList.vue";

/*eslint-disable*/
export default {
  name: "prod-ucts",
  props: [
    "products",
    "country",
    "maximum",
    "cart",
    "cartQty",
    "cartTotal",
    "sliderStatus",
    "sliderState"
  ],
  components: {
    Navbar,
    PriceSlider,
    ProductList
  }
};
</script>
