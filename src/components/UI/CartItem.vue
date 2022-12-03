<template>
  <article class="cart-item">
    <img src="/images/Cart/ProductInCart.svg" alt="cart-item-img" />
    <section class="cart-item-desc">
      <h3>{{ props.productName }}</h3>
      <p v-if="props.productColor">
        Color: <span>{{ props.productColor }}</span>
      </p>
      <p v-if="props.productSize">
        Size: <span>{{ props.productSize }}</span>
      </p>
      <article class="cart-item-price">
        <span
          class="cart-item-real-price"
          :class="{ 'inactive-price': props.productOffPrice }"
          >${{ props.productPrice }}</span
        >
        <span class="cart-item-off-price" v-if="!!props.productOffPrice">
          ${{ props.productOffPrice }}
        </span>
      </article>
    </section>
    <!-- <article class="cart-item-price">
      <span class="cart-item-real-price">${{ props.productPrice }}</span>
      <span class="cart-item-off-price">${{ props.productOffPrice }}</span>
    </article> -->
    <article class="cart-item-qty">
      <label :for="`qty-${props.productId}`">Quantity:</label>
      <input
        type="number"
        :id="`qty-${props.productId}`"
        class="cart-item-quantity"
        v-model="qty"
        min="0"
        @input="onUpdate"
      />
    </article>
    <button @click="onDelete">
      <Close />
    </button>
  </article>
</template>
<script setup>
import { ref } from "vue";
import Close from "../icons/Close.vue";

const emits = defineEmits(["onDelete", "onUpdate"]);
const props = defineProps([
  "productId",
  "productName",
  "productColor",
  "productSize",
  "productPrice",
  "productOffPrice",
  "qty",
]);
// for immutable prop
const qty = ref(props.qty);

function onDelete() {
  emits("onDelete", props.productId);
}

function onUpdate() {
  emits("onUpdate", { qty: qty.value, ID: props.productId });
}
</script>
