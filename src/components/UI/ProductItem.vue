<template>
  <article class="product-card">
    <img
      class="product-img"
      src="/images/Home/Technology.svg"
      alt="product-img"
    />
    <section class="product-detail">
      <h4 class="product-title">Gigabyte AX-370 Gaming K7</h4>
      <p class="product-description">GIGA-BYTE Technology Co</p>
      <section class="product-rating-price">
        <section class="product-rating">
          <img class="star-img" src="/images/common/Star.svg" alt="rating" />
          <span class="star-amount">4.7</span>
        </section>
        <span class="review-amount">24 reviews</span>
        <section class="product-price">
          <span class="last-price">$398</span>
          <span class="new-price">$310</span>
        </section>
      </section>
    </section>
    <section class="product-overlay">
      <button><heart /></button>
      <button><share /></button>
      <button><bookmark /></button>
    </section>
  </article>
</template>

<script setup>
import heart from "../icons/ProductItem/Heart.vue";
import share from "../icons/ProductItem/Share.vue";
import bookmark from "../icons/ProductItem/Bookmark.vue";
</script>
