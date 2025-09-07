<template>
  <div class="item">
    <div :class="isActive ? 'active-border' : ''" class="item-img ">
      <img :src="item.image.desktop" :alt="item.name">
    </div>
    <div class="item-button">
      <app-button
        :is-active="isActive"
        :item="item"
        @add-to-cart="$emit('add-to-cart', item)"
      ></app-button>
    </div>
    <div class="item-name grey-color">{{item.name}}</div>
    <div class="item-category dark-color bold-text">{{item.category}}</div>
    <div class="item-price red-text bold-text">${{Number(item.price).toFixed(2)}}</div>
  </div>
</template>

<script setup>
import {defineProps, defineEmits} from "vue"
  import AppButton from "@/components/AppButton.vue";

  defineProps({
    item: {
      type: Object
    },
    isActive: {
      type: Boolean
    }
  })

  defineEmits(['add-to-cart'])


</script>


<style scoped>
  .item{
    width: 32%;
    position: relative;
  }
  .item-img{
    width: 240px;
    height: 240px;
    border-radius: 10px;
    overflow: hidden;
  }
  .item img{
    width: 100%;
    height: 100%;
    object-fit: cover;
  }
  .item-button{
    position: absolute;
    top: 215px;
    left: 0;
    width: 100%;
  }
  .item-name{
    margin-top: 30px;
    font-size: 16px;
  }
  @media(max-width: 992px){
    .item{
      width: 48%;
    }
    .item-button{
      width: auto;
      left: 35px;
    }
  }
</style>