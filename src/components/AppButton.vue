<template>
  <div class="button-wrap">
    <button v-if="!props.isActive" class="button" @click="addToCart">
      <span>
        <svg width="24" height="24" viewBox="0 0 24 24" fill="hsl(14, 86%, 42%)">
      <path d="M7 18c-1.1 0-1.99.9-1.99 2S5.9 22 7 22s2-.9 2-2-.9-2-2-2zM1 2v2h2l3.6 7.59-1.35 2.45c-.16.28-.25.61-.25.96 0 1.1.9 2 2 2h12v-2H7.42c-.14 0-.25-.11-.25-.25l.03-.12.9-1.63h7.45c.75 0 1.41-.41 1.75-1.03l3.58-6.49A1.003 1.003 0 0020 4H5.21l-.94-2H1zm16 16c-1.1 0-1.99.9-1.99 2s.89 2 1.99 2 2-.9 2-2-.9-2-2-2z"/>
        </svg>
      </span>
      Add to Cart
    </button>
    <div v-else class="button button-quantity">
      <button class="button-minus" @click="removeOneItem(props.item)">
        <div>
          <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
            <circle cx="12" cy="12" r="10" stroke="white" stroke-width="2" fill="none"/>
            <path d="M8 12H16" stroke="white" stroke-width="2" stroke-linecap="round"/>
          </svg>
        </div>
      </button>
      <span>{{ quntityOnBtn }}</span>
      <button class="button-plus" @click="addToCart">
        <div>
          <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
            <circle cx="12" cy="12" r="10" stroke="white" stroke-width="2" fill="none"/>
            <path d="M12 8V16M8 12H16" stroke="white" stroke-width="2" stroke-linecap="round"/>
          </svg>
        </div>
      </button>
    </div>
  </div>
</template>

<script setup>
import {defineProps, defineEmits, inject, computed} from "vue"

  const props = defineProps({
    item: {
      type: Object
    },
    isActive: {
      type: Boolean,
      default: false
    }
  })

  const cartItems = inject("cart-items")

  const quntityOnBtn = computed(() => {
    if (cartItems.value) {
      const item = cartItems.value.find(cartItem => cartItem.name === props.item.name)
      return item ? item.quantity : 0
    }
    return 0
  })

  const emit = defineEmits(['add-to-cart','remove-one-item'])

  const addToCart = () => {
    emit('add-to-cart', props.item)
  }

  const removeOneItem = inject("remove-one-item")
</script>


<style scoped>
.item-button button{
  display: block;
  margin: 0 auto;
}
.button{
  color: hsl(14, 65%, 9%);
  font-weight: bold;
  font-size: 17px;
}
.button-quantity{
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: hsl(14, 86%, 42%);
}
.button-quantity button{
  background-color: hsl(14, 86%, 42%);
  width: 30px;
  scale: 1;
  transition: .3s ease-in-out;
}
.button-quantity span{
  color: white;
}
.button-quantity button:hover{
  scale: 1.1;
}
.button-minus, .button-plus{
  padding: 0;
}
.button-minus div{
  display: flex;
  justify-content: start;
}
.button-plus div{
  display: flex;
  justify-content: end;
}
@media(max-width: 992px){
  .button-wrap{
    width: 100%;
  }
  .button-wrap button{
    padding-left: 20px;
    padding-right: 20px;
  }
  .button-quantity{
    width: 165px;
  }
  .button-quantity > button{
    padding-left: 0px;
    padding-right: 0px;
  }
  .button{
    font-size: 16px;
  }
}
</style>