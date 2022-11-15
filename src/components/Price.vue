<template>
<span>{{this.prefix + Number.parseFloat(this.value*this.conversion).toFixed(this.precision)}}</span>

  
</template>

<script>
export default {
    name:"pri-ce",
    props:{
    value:Number,
    prefix:{
      type:String,
      default:'$'
    },
    conversion:{
      type:Number,
      default:1
    },
    precision:{
      type:Number,
      default:2
    }
  }
};
</script>

<style>

</style>