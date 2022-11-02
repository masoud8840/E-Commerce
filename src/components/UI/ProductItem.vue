<template>
  <article class="product-card">
    <img
      class="product-img"
      :src="`/images/Home/${props.productImg}`"
      alt="product-img"
    />
    <section class="product-detail">
      <h4 class="product-title">{{ props.productName }}</h4>
      <p class="product-description">{{ props.productDescription }}</p>
      <section class="product-rating-price">
        <section class="product-rating">
          <img class="star-img" src="/images/common/Star.svg" alt="rating" />
          <span class="star-amount">{{ props.productRating }}</span>
        </section>
        <span class="review-amount">{{ props.productReview }} reviews</span>
        <section class="product-price">
          <span class="last-price" v-if="props.productLastPrice"
            >${{ props.productLastPrice }}</span
          >
          <span class="new-price">${{ props.productNewPrice }}</span>
        </section>
      </section>
    </section>
    <section class="product-overlay">
      <button :class="{ active: props.isLiked }"><heart /></button>
      <button><share /></button>
      <button :class="{ active: props.isBookmarked }"><bookmark /></button>
    </section>
  </article>
</template>

<script setup>
import heart from "../icons/ProductItem/Heart.vue";
import share from "../icons/ProductItem/Share.vue";
import bookmark from "../icons/ProductItem/Bookmark.vue";
const props = defineProps([
  "productName",
  "productDescription",
  "productRating",
  "productReview",
  "productLastPrice",
  "productNewPrice",
  "productImg",
  "isLiked",
  "isBookmarked",
]);
</script>
