<template>
  <div class="cart-item__container">
    <div>
      <div class="cart-item__name dark-color bold-text">
        {{item.category}}
      </div>
      <div class="cart-item__info">
        <div class="cart-item__quantity red-text bold-text">{{item.quantity}}</div>
        <div class="cart-item__price grey-color">@ ${{Number(item.price).toFixed(2)}}</div>
        <div class="cart-item__total-price darkgrey-color">${{Number(item.price * item.quantity).toFixed(2)}}</div>
      </div>
    </div>
    <div class="cart-item__close" @click="removeItem(item.name)">
      <div>
        <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
          <circle cx="12" cy="12" r="10" stroke="grey" stroke-width="2" fill="none"/>
          <path d="M12 8V16M8 12H16" stroke="grey" stroke-width="2" stroke-linecap="round"/>
        </svg>
      </div>
    </div>
  </div>
  <hr>
</template>


<script setup>
  import {defineProps, inject} from "vue"

  defineProps({
    item: {
      type: Object,
      required: true
    }
  })

  // const cartItems = inject("cart-items");
  const removeItem = inject("remove-item");

</script>


<style scoped>
  .cart-item__container,.cart-item__info{
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  .cart-item__container{
    background-color: white;
    transition: .3s ease-in-out;
    padding: 5px;
  }
  .cart-item__container:hover{
    background-color: #f5f5f5;
    border-radius: 5px;
    overflow: hidden;
  }
  .cart-item__price{
    margin: 0 15px;
  }
  .cart-item__close div{
    transform: rotate(45deg);
    transform-origin: center;
    cursor: pointer;
    scale: 1;
    transition: .3s ease-in-out;
  }
  .cart-item__close div:hover{
    scale: 1.1;
  }
  hr{
    margin-top: 0px;
  }
</style>