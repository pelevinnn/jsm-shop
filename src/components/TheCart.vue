<template>
  <div class="cart-wrapper" v-if="cartItems.length > 0">
    <h2 class="red-text bold-text">Your Cart({{cartItems.length}})</h2>
    <app-cart-item
      v-for="(item, index) in props.cartItems"
      :key="index"
      :item="item"
    ></app-cart-item>
    <div class="cart-price">
      <p>Order Total</p>
      <div class="dark-color bold-text">${{Number(props.totalPrice).toFixed(2)}}</div>
    </div>
    <div class="cart-delivery">
      <svg xmlns="http://www.w3.org/2000/svg" width="21" height="20" fill="none" viewBox="0 0 21 20"><path fill="#1EA575" d="M8 18.75H6.125V17.5H8V9.729L5.803 8.41l.644-1.072 2.196 1.318a1.256 1.256 0 0 1 .607 1.072V17.5A1.25 1.25 0 0 1 8 18.75Z"/><path fill="#1EA575" d="M14.25 18.75h-1.875a1.25 1.25 0 0 1-1.25-1.25v-6.875h3.75a2.498 2.498 0 0 0 2.488-2.747 2.594 2.594 0 0 0-2.622-2.253h-.99l-.11-.487C13.283 3.56 11.769 2.5 9.875 2.5a3.762 3.762 0 0 0-3.4 2.179l-.194.417-.54-.072A1.876 1.876 0 0 0 5.5 5a2.5 2.5 0 1 0 0 5v1.25a3.75 3.75 0 0 1 0-7.5h.05a5.019 5.019 0 0 1 4.325-2.5c2.3 0 4.182 1.236 4.845 3.125h.02a3.852 3.852 0 0 1 3.868 3.384 3.75 3.75 0 0 1-3.733 4.116h-2.5V17.5h1.875v1.25Z"/></svg>
      This is a&nbsp;<b>carbon-neutral</b>&nbsp;delivery
    </div>
    <div class="cart-button">
      <button class="">Confirm Order</button>
    </div>
  </div>
  <div class="cart-wrapper" v-else>
    <h2 class="red-text bold-text">Your Cart Empty</h2>
  </div>
</template>

<script setup>
  import AppCartItem from "@/components/AppCartItem.vue"
  import {defineProps} from "vue"

  const props = defineProps({
    cartItems:{
      type: Array
    },
    totalPrice:{
      type: Number
    }
  })

  // watch( props.totalPrice, () => {
  //   console.log(props.totalPrice)
  // } )
</script>

<style scoped>
  .cart-price{
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  .cart-wrapper{
    padding: 30px 20px;
    background-color: white;
    border-radius: 10px;
    overflow: hidden;
  }
  h2{
    margin-bottom: 20px;
  }
  .cart-price > div{
    font-size: 32px;
  }
  .cart-price p{
    margin-bottom: 0px;
  }
  .cart-delivery{
    line-height: 3;
    width: 100%;
    text-align: center;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: hsl(13, 31%, 94%);
    border-radius: 10px;
    overflow: hidden;
    margin-bottom: 24px;
  }
  .cart-button{
    width: 100%;
    overflow: hidden;
  }
  .cart-button > button{
    border-radius: 30px;
    width: 100%;
    background-color: hsl(14, 86%, 42%);
    color: white;
    border: 2px solid hsl(14, 86%, 42%);
    line-height: 3;
    transition: .3s ease-in-out;
  }
  .cart-button > button:hover{
    background-color: white;
    color: hsl(14, 86%, 42%);
  }
  @media(max-width: 992px){
    .cart-wrapper h2{
      font-size: 24px;
      margin-bottom: 0;
    }
    .cart-price > div{
      font-size: 24px;
    }
    .cart-delivery{
      font-size: 12px;
    }
  }
</style>