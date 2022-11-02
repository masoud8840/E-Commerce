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
      <product-item></product-item>
    </article>
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
</script>
