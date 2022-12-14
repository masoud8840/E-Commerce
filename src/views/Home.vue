<template>
  <header class="main-header">
    <form class="header-overlay" autocomplete="off">
      <div class="container">
        <h3 class="header-title">Explore and Find everything you need!</h3>
        <p class="header-subtitle">over <span>7,500,000</span> stuff</p>
        <input
          :class="setSearchInputStyle"
          type="text"
          name="search"
          id="search-product-input"
          placeholder="find something..."
          v-model="searchValue"
        />
      </div>
    </form>
  </header>
  <section class="subheader container">
    <article v-for="item in subheaderItems">
      <img :src="item.imgUrl" :alt="item.title" />
      <h4>{{ item.title }}</h4>
      <p>{{ item.subtitle }}</p>
    </article>
  </section>

  <section class="our-categories container">
    <header>
      <h3 class="our-categories-title">Our Categories</h3>
      <p class="our-categories-subtitle">Here you can find almost everything</p>
    </header>
    <article class="main-content">
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
    <flicking
      ref="discountedListFlicking"
      class="discount-list"
      :options="{
        align: 'prev',
        circularFallback: 'linear',
        moveType: 'freeScroll',
      }"
    >
      <product-item
        v-for="(prod, index) in discountedProducts"
        :key="index"
        :product-id="prod.ID"
        :product-name="prod.name"
        :product-brand="prod.brand"
        :product-img="prod.img"
        :product-rating="prod.rating"
        :product-review="prod.review"
        :product-price="prod.price"
        :product-discount="prod.discount"
        :is-liked="prod.isLiked"
        :is-bookmarked="prod.isBookmarked"
        :creator-company="prod.creatorCompany"
        @on-product-like="likeProduct"
        @on-product-bookmark="bookmarkProduct"
      ></product-item>
    </flicking>
    <footer class="discount-arrows">
      <button @click="goToPrevSlide">
        <arrow-left />
      </button>
      <button @click="goToNextSlide">
        <arrow-right />
      </button>
    </footer>
  </section>

  <section class="some-stuff container">
    <header>
      <h3 class="some-stuff-title">Some Of Our Stuff</h3>
      <p class="some-stuff-subtitle">Take a quick look at our stuff</p>
      <nav class="container">
        <ul>
          <li v-for="el in navElements">
            <button
              @click="changeNavbarUnderlineStyle(el.shorthand)"
              class="nav-btn"
              :class="{ active: navActiveElem === el.shorthand }"
            >
              {{ el.text }}
            </button>
          </li>
        </ul>
        <!-- <div class="underline" :style="getNavbarUnderlineStyle"></div> -->
      </nav>
    </header>
    <transition name="some-stuff">
      <article class="some-stuff-list main-content" v-if="isStuffLoaded">
        <product-item
          v-for="(prod, index) in categorizedProducts"
          :key="index"
          :product-id="prod.ID"
          :product-name="prod.name"
          :product-brand="prod.brand"
          :product-img="prod.img"
          :product-rating="prod.rating"
          :product-review="prod.review"
          :product-price="prod.price"
          :is-liked="prod.isLiked"
          :is-bookmarked="prod.isBookmarked"
          :creator-company="prod.creatorCompany"
          @on-product-like="likeProduct"
          @on-product-bookmark="bookmarkProduct"
        ></product-item>
      </article>
    </transition>
  </section>
</template>

<script setup>
import Flicking from "@egjs/vue3-flicking";
import ProductItem from "../components/UI/ProductItem.vue";
import ArrowLeft from "../components/icons/Common/ArrowLeft.vue";
import ArrowRight from "../components/icons/Common/ArrowRight.vue";
import { ref, computed, inject } from "vue";
const discountedListFlicking = ref(null);

function goToPrevSlide() {
  discountedListFlicking.value.prev();
}
function goToNextSlide() {
  discountedListFlicking.value.next();
}
const searchValue = ref("");
const setSearchInputStyle = computed(() =>
  searchValue.value.trim() !== "" ? "bg-white" : ""
);
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

const products = inject("products");

function likeProduct(prodID) {
  // we don't have api yet, so will iterate though all objects
  products.value.map((prod) => {
    if (prod.ID === prodID) prod.isLiked = !prod.isLiked;
  });
}
function bookmarkProduct(prodID) {
  // we don't have api yet, so will iterate though all objects
  products.value.map((prod) => {
    if (prod.ID === prodID) prod.isBookmarked = !prod.isBookmarked;
  });
}

// some of our stuff
const navActiveElem = ref("electronics");
const navElements = ref([
  {
    text: "Electronics",
    shorthand: "electronics",
  },
  {
    text: "Home & Kitchen",
    shorthand: "h&k",
  },
  {
    text: "Car & Tools",
    shorthand: "c&t",
  },
  {
    text: "Health & Beauty",
    shorthand: "h&b",
  },
  {
    text: "Fashion & Clothing",
    shorthand: "f&c",
  },
  {
    text: "Books & Stationary",
    shorthand: "b&s",
  },
]);

const isStuffLoaded = ref(true);
function changeNavbarUnderlineStyle(currentTab) {
  navActiveElem.value = currentTab;
  isStuffLoaded.value = false;
  setTimeout(() => {
    isStuffLoaded.value = true;
  }, 450);
}

const discountedProducts = computed(() => {
  const discountedProds = products.value.filter((prod) => prod.discount);
  return discountedProds.slice(0, 9);
});

const categorizedProducts = computed(() => {
  return products.value.filter((prod) => prod.cat === navActiveElem.value);
});
</script>
