<template>
  <div>
    <h1>Checkout</h1>

    <table class="table table-hover" v-if="cart.length">
      <caption class="text-right h3">
        <b>Total:</b>
        <price class="d-block text-success font-weight-light" :value="Number(cartTotal * ((100-sale)/100))"></price>

      </caption>
      <thead>
        <tr>
          <th scope="col"></th>
          <th scope="col">Item</th>
          <th scope="col" class="text-center">Qty</th>
          <th scope="col" class="text-right">Price</th>
          <th scope="col" class="text-right">Sub-total</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, index) in cart" :key="item.product.id">
          <td class="text-center">
            <div class="btn-group" role="group" aria-label="Basic example">
              <button @click="$emit('add', item.product)" class="btn btn-info">+</button>
              <button @click="$emit('delete', index)" class="btn btn-outline-info">-</button>
            </div>
          </td>
          <th scope="row">{{item.product.name}}</th>
          <td class="text-center">{{item.qty}}</td>
          <td class="text-right">{{Number(item.product.price)}}</td>
          <td class="text-right">{{Number((item.qty * item.product.price) * (100-sale)/100)}}</td>
        </tr>
      </tbody>
    </table>
    <!--eslint-disable-->
    <div class="divider" v-if="cart.length">
      <div class="title">Enter promo code "sale", "newYear"  - sale will be calculated</div>
      <p>
        <input class="form-control" type="text" v-model="promo" @input="$emit('update:promoCode',promo)" placeholder="Enter promo code"/>
      </p>
      <p>
        <div class="alert alert-success">Your sale is {{ sale }}%</div>
      </p>
    </div>
    <router-link class="btn btn-sm btn-outline-info text-dark" to="/">Keep Shopping</router-link>
  </div>
</template>

<script>
import Price from "./Price.vue";
import VueRouter from "vue-router";

export default {
  name: "checkout",
  data:function(){
    return{
      promo:""
    }
  },
  props: ["cart", "cartTotal","sale","promoCode"],
  components: {
    Price
  }
};
</script>

<style>
.divider{

	max-width: 400px;
	margin: 40px auto;
	font-size: 14px;
	font-family: 'Open Sans', sans-serif;
	padding: 0 20px;
}

.title{

	font-weight: bold;
	margin-bottom: 5px;
}
</style>

