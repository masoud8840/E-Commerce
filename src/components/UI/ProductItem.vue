<template>
  <article class="product-card">
    <img
      class="product-img"
      :src="`/images/products/${props.productImg}`"
      alt="product-img"
    />
    <section class="product-detail">
      <router-link :to="`/product/${props.productName}`">
        <h4 class="product-title">{{ props.productName }}</h4>
      </router-link>
      <router-link :to="`company/${props.creatorCompany}`">
        <p class="product-description">{{ props.productBrand }}</p>
      </router-link>
      <section class="product-rating-price">
        <section class="product-rating">
          <img class="star-img" src="/images/common/Star.svg" alt="rating" />
          <span class="star-amount">{{ props.productRating }}</span>
        </section>
        <span class="review-amount">{{ props.productReview }} reviews</span>
        <section class="product-price">
          <span class="last-price" v-if="props.productDiscount">
            ${{ props.productPrice }}
          </span>
          <span class="new-price">${{ discountPrice }}</span>
        </section>
      </section>
    </section>
    <section class="product-overlay">
      <button :class="{ active: props.isLiked }" @click="likeProduct">
        <heart />
      </button>
      <button @click="shareProduct"><share /></button>
      <button :class="{ active: props.isBookmarked }" @click="bookmarkProduct">
        <bookmark />
      </button>
    </section>
  </article>
</template>

<script setup>
import { ref } from "vue";
import heart from "../icons/ProductItem/Heart.vue";
import share from "../icons/ProductItem/Share.vue";
import bookmark from "../icons/ProductItem/Bookmark.vue";
const props = defineProps([
  "productId",
  "productName",
  "productBrand",
  "productRating",
  "productReview",
  "productPrice",
  "productDiscount",
  "productImg",
  "isLiked",
  "isBookmarked",
  "creatorCompany",
]);

const emits = defineEmits(["onProductLike", "onProductBookmark"]);

function likeProduct() {
  emits("onProductLike", props.productId);
}
function bookmarkProduct() {
  emits("onProductBookmark", props.productId);
}
// will edit later
function shareProduct() {
  const shareOptions = {
    url: "https://soft98.ir",
    title: "google.com",
    text: "Here is the google site",
  };
  if (navigator.share) {
    navigator.share(shareOptions).then(() => {
      console.log("Thanks for Sharing.");
    });
  } else {
    console.log("you don't have share ability");
  }
}

const discountPrice = ref(0);
if (props.productDiscount) {
  const calculatedPercent = (
    (props.productPrice * props.productDiscount) /
    100
  ).toFixed(2);
  discountPrice.value = props.productPrice - calculatedPercent;
} else {
  discountPrice.value = props.productPrice;
}
</script>
