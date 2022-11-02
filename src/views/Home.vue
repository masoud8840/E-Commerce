<template>
  <the-navigation></the-navigation>
  <section class="subheader container">
    <article v-for="item in subheaderItems">
      <img :src="item.imgUrl" :alt="item.title" />
      <h4>{{ item.title }}</h4>
      <p>{{ item.subtitle }}</p>
    </article>
  </section>

  <section class="our-categories container">
    <h3 class="our-categories-title">Our Categories</h3>
    <p class="our-categories-subtitle">Here you can find almost everything</p>
    <article>
      <section
        v-for="section in ourCategories"
        :class="`category-item category-${section.sectionClass}`"
      >
        <img :src="`/images/Home/${section.img}.svg`" :alt="section.img" />
        <div class="category-item-overlay">
          <h4 class="category-item-title">{{ section.title }}</h4>
          <p class="category-item-subtitle">{{ section.subtitle }}</p>
        </div>
      </section>
    </article>
  </section>

  <section class="discount container">
    <header>
      <h3 class="discount-title">Discount</h3>
      <router-link to="/">See More</router-link>
    </header>
    <article class="discount-list">
      <product-item
        v-for="(prod, index) in discountProducts"
        :key="index"
        :product-name="prod.name"
        :product-description="prod.description"
        :product-img="prod.img"
        :product-rating="prod.rating"
        :product-review="prod.review"
        :product-last-price="prod.lastPrice"
        :product-new-price="prod.newPrice"
        :is-liked="prod.isLiked"
        :is-bookmarked="prod.isBookmarked"
      ></product-item>
    </article>
    <footer class="discount-arrows">
      
    </footer>
  </section>
</template>

<script setup>
import TheNavigation from "../components/layout/TheNavigation.vue";
import ProductItem from "../components/UI/ProductItem.vue";
import { ref } from "vue";
const subheaderItems = ref([
  {
    imgUrl: "/images/Reliable.svg",
    title: "Reliable",
    subtitle: "Trusted by millions of users",
  },
  {
    imgUrl: "/images/Express.svg",
    title: "Express",
    subtitle: "1-Day arrival time",
  },
  {
    imgUrl: "/images/Guarantee.svg",
    title: "Guarantee",
    subtitle: "8 Days guarantee",
  },
]);

const ourCategories = ref([
  {
    sectionClass: "supermarket dark",
    img: "Supermarket",
    title: "Cooking Essentials",
    subtitle: "access fresh foods",
  },
  {
    sectionClass: "car dark",
    img: "Car",
    title: "Car",
    subtitle: "find any kind of in-car and out-car stuff",
  },
  {
    sectionClass: "cosmetic",
    img: "Cosmetics",
    title: "Cosmetics",
    subtitle: "feel better and fresh",
  },
  {
    sectionClass: "tv dark",
    img: "TV",
    title: "TVs",
    subtitle: "have everything on board",
  },
  {
    sectionClass: "technology",
    img: "Technology",
    title: "Technology",
    subtitle: "from smart watch to apple macbook",
  },
]);

const discountProducts = ref([
  {
    name: "Gigabyte AX-370 Gaming K7",
    description: "GIGA-BYTE Technology Co",
    rating: 4.5,
    review: 14,
    lastPrice: 189,
    newPrice: 102,
    img: "Car.svg",
    isBookmarked: false,
    isLiked: false,
  },
  {
    name: "Gigabyte AX-370 Gaming K7",
    description: "GIGA-BYTE Technology Co",
    rating: 4.5,
    review: 14,
    lastPrice: 189,
    newPrice: 102,
    img: "Car.svg",
    isBookmarked: false,
    isLiked: false,
  },
  {
    name: "Gigabyte AX-370 Gaming K7",
    description: "GIGA-BYTE Technology Co",
    rating: 4.5,
    review: 14,
    lastPrice: 189,
    newPrice: 102,
    img: "Car.svg",
    isBookmarked: true,
    isLiked: false,
  },
  {
    name: "Gigabyte AX-370 Gaming K7",
    description: "GIGA-BYTE Technology Co",
    rating: 4.2,
    review: 10,
    lastPrice: 95,
    newPrice: 58,
    img: "Supermarket.svg",
    isBookmarked: true,
    isLiked: true,
  },
]);
</script>
