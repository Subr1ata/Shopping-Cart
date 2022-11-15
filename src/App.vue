<template>
  <div id="app" class="container mt-5">
    <router-view :cart="cart" :cartQty="cartQty" :cartTotal="cartTotal" @delete="deleteItem" @add="addItem" @toggle="toggleSliderStatus" :sliderStatus="sliderStatus" :maximum.sync="maximum" :promoCode.sync="promoCode" :sale="sale" :country.sync="country" :products="products"></router-view>
  </div>
</template>

<script>

export default {
  name: 'App',
  data:function(){
    return{
      sliderStatus:true,
      maximum:99,
      country:"Europe",
      promoCode:'',
      cart:[],
      products:null
    };
  },
  mounted: function(){
      fetch("https://hplussport.com/api/products/order/price")
      .then(response => response.json())
      .then(data => {
        this.products = data
      })
    },
    computed:{
      cartTotal:function(){
        let sum=0;
        for(let key in this.cart){
          sum = sum + (this.cart[key].product.price * this.cart[key].qty);
          // sum = sum + `<price></price>`;
        }
        return sum;

      },
      cartQty:function(){
        let qty=0;
        for(let key in this.cart){
          qty = qty + (this.cart[key].qty);
        }
        return qty;
      },
      sale:function(){
        let codes = {
          newYear: 10,
          sale: 20
        };
        
        let sale = ( codes[this.promoCode] != undefined) ? codes[this.promoCode] : 0;
        
        return sale;
		  }
    },
    methods:{
      toggleSliderStatus:function(){
        this.sliderStatus = !this.sliderStatus;
      },
      deleteItem:function(idx){
        if(this.cart[idx].qty > 1){
          this.cart[idx].qty--;
        }else{
          this.cart.splice(idx,1);
        }
      },
      addItem:function(product){
        var whichProduct;
        var existing = this.cart.filter(function(item,index){
          if(item.product.id == Number(product.id)){
            whichProduct = index;
            return true;
          }else{
            return false;
          }
        })
        if(existing.length){
          this.cart[whichProduct].qty++;
        }else{
          this.cart.push({product:product, qty:1});
        }
      }
    },
}
</script>
