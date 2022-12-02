<template>
  <section class="cart-view">
    <div class="cart-view-inner container">
      <section class="cart-list">
        <h3>Order</h3>
        <article class="cart-list-inner"></article>
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
              <span>$254</span>
            </section>
            <section class="additional-service-amount">
              <h5>Additional Service</h5>
              <span>$12</span>
            </section>
            <section class="total-amount">
              <h4>TOTAL</h4>
              <span>$266</span>
            </section>
          </article>
          <button type="button" class="checkout-btn">Checkout</button>
        </article>
      </section>
    </div>
  </section>
</template>
