<template>
  <div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header">
          <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"><svg data-v-4eb748d8="" width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg"><circle data-v-4eb748d8="" cx="12" cy="12" r="10" stroke="grey" stroke-width="2" fill="none"></circle><path data-v-4eb748d8="" d="M12 8V16M8 12H16" stroke="grey" stroke-width="2" stroke-linecap="round"></path></svg></button>
        </div>
        <div class="modal-body dark-color">
          Do you confirm your order?
        </div>
        <div class="modal-footer cart-button">
          <button type="button" class="btn btn-secondary" data-bs-dismiss="modal" @click="cartItems">Yes</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
  import {inject} from "vue";

  const cartItems = inject("remove-cart")

</script>


<style scoped>
.cart-button > button{
  border-radius: 30px;
  width: 30%;
  background-color: hsl(14, 86%, 42%);
  color: white;
  border: 2px solid hsl(14, 86%, 42%);
  line-height: 2;
  transition: .3s ease-in-out;
}
.cart-button > button:hover {
  background-color: white;
  color: hsl(14, 86%, 42%);
}
.btn-close{
  background: transparent;
  transform: rotate(45deg);

}
.modal-body{
  font-family: 'RedHatText', sans-serif;
  font-size: 18px;
  font-weight: bold;
}
</style>