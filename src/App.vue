<template>
  <div class="row">
    <div class="col-md-8">
      <h1 class="dark-color">Desserts</h1>
      <div class="items">
        <app-item
            v-for="(item, index) in items"
            :key="index"
            :item="item"
            :is-active="cartItems.some(cartItem => cartItem.name === item.name)"
            @add-to-cart="addToCart"
        ></app-item>
      </div>
    </div>
    <div class="col-md-4">
      <the-cart
        :cart-items="cartItems"
        :total-price="totalPrice"
      ></the-cart>
    </div>
  </div>
</template>

<script setup>
  import AppItem from "@/components/AppItem.vue";
  import TheCart from "@/components/TheCart.vue";
  import {ref, provide, computed} from "vue";

  const items = ref([
    {
      "image": {
        "thumbnail": "./assets/images/image-waffle-thumbnail.jpg",
        "mobile": "./assets/images/image-waffle-mobile.jpg",
        "tablet": "./assets/images/image-waffle-tablet.jpg",
        "desktop": "./assets/images/image-waffle-desktop.jpg"
      },
      "name": "Waffle with Berries",
      "category": "Waffle",
      "price": 6.50
    },
    {
      "image": {
        "thumbnail": "./assets/images/image-creme-brulee-thumbnail.jpg",
        "mobile": "./assets/images/image-creme-brulee-mobile.jpg",
        "tablet": "./assets/images/image-creme-brulee-tablet.jpg",
        "desktop": "./assets/images/image-creme-brulee-desktop.jpg"
      },
      "name": "Vanilla Bean Crème Brûlée",
      "category": "Crème Brûlée",
      "price": 7.00
    },
    {
      "image": {
        "thumbnail": "./assets/images/image-macaron-thumbnail.jpg",
        "mobile": "./assets/images/image-macaron-mobile.jpg",
        "tablet": "./assets/images/image-macaron-tablet.jpg",
        "desktop": "./assets/images/image-macaron-desktop.jpg"
      },
      "name": "Macaron Mix of Five",
      "category": "Macaron",
      "price": 8.00
    },
    {
      "image": {
        "thumbnail": "./assets/images/image-tiramisu-thumbnail.jpg",
        "mobile": "./assets/images/image-tiramisu-mobile.jpg",
        "tablet": "./assets/images/image-tiramisu-tablet.jpg",
        "desktop": "./assets/images/image-tiramisu-desktop.jpg"
      },
      "name": "Classic Tiramisu",
      "category": "Tiramisu",
      "price": 5.50
    },
    {
      "image": {
        "thumbnail": "./assets/images/image-baklava-thumbnail.jpg",
        "mobile": "./assets/images/image-baklava-mobile.jpg",
        "tablet": "./assets/images/image-baklava-tablet.jpg",
        "desktop": "./assets/images/image-baklava-desktop.jpg"
      },
      "name": "Pistachio Baklava",
      "category": "Baklava",
      "price": 4.00
    },
    {
      "image": {
        "thumbnail": "./assets/images/image-meringue-thumbnail.jpg",
        "mobile": "./assets/images/image-meringue-mobile.jpg",
        "tablet": "./assets/images/image-meringue-tablet.jpg",
        "desktop": "./assets/images/image-meringue-desktop.jpg"
      },
      "name": "Lemon Meringue Pie",
      "category": "Pie",
      "price": 5.00
    },
    {
      "image": {
        "thumbnail": "./assets/images/image-cake-thumbnail.jpg",
        "mobile": "./assets/images/image-cake-mobile.jpg",
        "tablet": "./assets/images/image-cake-tablet.jpg",
        "desktop": "./assets/images/image-cake-desktop.jpg"
      },
      "name": "Red Velvet Cake",
      "category": "Cake",
      "price": 4.50
    },
    {
      "image": {
        "thumbnail": "./assets/images/image-brownie-thumbnail.jpg",
        "mobile": "./assets/images/image-brownie-mobile.jpg",
        "tablet": "./assets/images/image-brownie-tablet.jpg",
        "desktop": "./assets/images/image-brownie-desktop.jpg"
      },
      "name": "Salted Caramel Brownie",
      "category": "Brownie",
      "price": 4.50
    },
    {
      "image": {
        "thumbnail": "./assets/images/image-panna-cotta-thumbnail.jpg",
        "mobile": "./assets/images/image-panna-cotta-mobile.jpg",
        "tablet": "./assets/images/image-panna-cotta-tablet.jpg",
        "desktop": "./assets/images/image-panna-cotta-desktop.jpg"
      },
      "name": "Vanilla Panna Cotta",
      "category": "Panna Cotta",
      "price": 6.50
    }
  ])

  const cartItems = ref([])

  const addToCart = (item) => {
    const isItemInCart = cartItems.value.some(cartItem => cartItem.name === item.name)
    if(isItemInCart){
      const cartItemValue = cartItems.value.find( cartItem => cartItem.name === item.name )
      // console.log(cartItemValue);
      cartItemValue.quantity++
    } else {
      cartItems.value.push({...item, quantity: 1})
    }
    // console.log(isItemInCart);
  }

  const removeOneItemFromCart = (item) => {
    // console.log(item)
    const isItemInCart = cartItems.value.some(cartItem => cartItem.name === item.name)
    if(isItemInCart){
      const cartItemValue = cartItems.value.find( cartItem => cartItem.name === item.name )
      console.log(cartItemValue);
      cartItemValue.quantity--
      if( cartItemValue.quantity == 0 ){
        removeFromCart(cartItemValue.name)
      }
    } else {
      console.log('корзина в ошибке по количеству')
      return false
    }
  }

  function removeFromCart(name){
    cartItems.value = cartItems.value.filter( item => item.name !== name )
  }

  const totalPrice = computed(() => {
    if(cartItems.value.length < 1){
      return 0
    }
    const prices = cartItems.value.map(item => item.price * item.quantity)
    return prices.reduce((acc, curr) => acc + curr, 0)
  })

  provide('cart-items', cartItems)
  provide('remove-item', removeFromCart)
  provide('remove-one-item', removeOneItemFromCart)

</script>

<style>
  .items{
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-wrap: wrap;
    gap: 10px;
  }
  .row{
    margin-top: 50px;
  }
  h1{
    font-weight: bold;
  }
</style>
