<template>
  <section class="cart-view">
    <div class="container empty-cart-screen" v-if="productsInCart.length === 0">
      <Cart class="empty-cart-icon" />
      <div>
        <h3>There is no product in you'r cart.</h3>
        <router-link to="/product/list"> Add Product</router-link>
      </div>
    </div>
    <div class="cart-view-inner container" v-if="productsInCart.length !== 0">
      <section class="cart-list">
        <h3>Order</h3>
        <article class="cart-list-inner">
          <cart-item
            v-for="prod in productsInCart"
            :key="prod"
            :product-id="prod.id"
            :product-name="prod.name"
            :product-size="prod.size"
            :product-color="prod.color"
            :product-price="prod.realPrice"
            :product-off-price="prod.offPrice"
            :qty="prod.qty"
            @on-delete="deleteCartItem"
            @on-update="updateCartItem"
          ></cart-item>
        </article>
      </section>
      <section class="payment-summary">
        <h3>payment summary</h3>
        <article class="payment-summary-inner">
          <section class="transaction-code">
            <h4>Transaction code</h4>
            <span>VC11685sk</span>
          </section>
          <section class="coupon-code">
            <input
              type="text"
              id="couponCode"
              class="coupon-code-input"
              placeholder="coupon code here"
            />
            <button type="button" class="coupon-code-btn">Apply</button>
          </section>
          <article class="payment-summary-recipt">
            <section class="order-summary-amount">
              <h5>Order Summary</h5>
              <span>${{ updateTotalPrice - additionalServices }}</span>
            </section>
            <section class="additional-service-amount">
              <h5>Additional Service</h5>
              <span>${{ additionalServices }}</span>
            </section>
            <section class="total-amount">
              <h4>TOTAL</h4>
              <span>${{ updateTotalPrice }}</span>
            </section>
          </article>
          <button type="button" class="checkout-btn">Checkout</button>
        </article>
      </section>
    </div>
  </section>
</template>

<script setup>
import CartItem from "../components/UI/CartItem.vue";
import Cart from "../components/icons/Cart.vue";
import { ref, computed } from "vue";

const productsInCart = ref([
  {
    id: 1,
    name: "Rust copper silk slip dress",
    color: "black/white",
    size: "MD",
    realPrice: 192,
    offPrice: 154,
    qty: 2,
  },
  {
    id: 2,
    name: "Rust copper silk slip dress",
    color: "black/white",
    size: "MD",
    realPrice: 192,
    offPrice: 134,
    qty: 1,
  },
  {
    id: 3,
    name: "Rust copper silk slip dress",
    color: "black/white",
    size: "MD",
    realPrice: 192,
    offPrice: null,
    qty: 1,
  },
]);

const additionalServices = ref(32);

function deleteCartItem(prodId) {
  productsInCart.value = productsInCart.value.filter(
    (prod) => prod.id !== prodId
  );
}
function updateCartItem(updatedProd) {
  productsInCart.value.map((prod) => {
    if (prod.id === updatedProd.ID) {
      prod.qty = updatedProd.qty;
      if (prod.qty < 1) deleteCartItem(updatedProd.ID);
    }
  });
}

const updateTotalPrice = computed(() => {
  let totalPrice = 0;
  productsInCart.value.map((prod) => {
    !!prod.offPrice
      ? (totalPrice += prod.qty * prod.offPrice)
      : (totalPrice += prod.qty * prod.realPrice);
  });

  totalPrice += additionalServices.value;

  return totalPrice;
});
</script>
