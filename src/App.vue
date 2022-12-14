<template>
  <the-navigation
    :force-toggle="toggleOff"
    @on-reset-force-toggle="resetForceToggle"
  ></the-navigation>
  <router-view @click="forceToggleOffNav"></router-view>
</template>

<script setup>
import { ref, provide } from "vue";
import TheNavigation from "./components/layout/TheNavigation.vue";

const toggleOff = ref(false);
function forceToggleOffNav() {
  toggleOff.value = true;
}

function resetForceToggle(forceToggleValue) {
  toggleOff.value = forceToggleValue;
}

const products = ref([
  {
    ID: 1,
    name: "Gigabyte AX-370 Gaming K7",
    brand: "GIGA-BYTE Technology Co",
    cat: "electronics",
    // discount percentage
    discount: 7.5,
    rating: 4.2,
    review: 10,
    price: 95,
    img: "electronics.jpg",
    isBookmarked: true,
    isLiked: true,
    creatorCompany: "gigabyte-technology-co",
  },
  {
    ID: 2,
    name: "Gigabyte AX-370 Gaming K5",
    brand: "GIGA-BYTE Technology Co",
    cat: "electronics",
    // discount percentage
    discount: 3.2,
    rating: 4.0,
    review: 17,
    price: 95,
    img: "electronics.jpg",
    isBookmarked: true,
    isLiked: true,
    creatorCompany: "gigabyte-technology-co",
  },
  {
    ID: 3,
    name: "Gigabyte AX-370 Gaming K3",
    brand: "GIGA-BYTE Technology Co",
    cat: "electronics",
    // discount percentage
    discount: 18,
    rating: 3.9,
    review: 34,
    price: 95,
    img: "electronics.jpg",
    isBookmarked: true,
    isLiked: true,
    creatorCompany: "gigabyte-technology-co",
  },
  {
    ID: 4,
    name: "ASUS Maximus Hero XII   ",
    brand: "ASUS Technology Co",
    cat: "electronics",
    // discount percentage
    discount: 6,
    rating: 4.5,
    review: 11,
    price: 95,
    img: "electronics.jpg",
    isBookmarked: true,
    isLiked: true,
    creatorCompany: "gigabyte-technology-co",
  },
  {
    ID: 5,
    name: "this is from H&K cat",
    brand: "H&K",
    cat: "h&k",
    // discount percentage
    discount: 10,
    rating: 4.5,
    review: 11,
    price: 240,
    img: "electronics.jpg",
    isBookmarked: true,
    isLiked: true,
    creatorCompany: "Company Name",
  },
  {
    ID: 6,
    name: "this is from H&K cat",
    brand: "H&K",
    cat: "h&k",
    // discount percentage
    discount: 10,
    rating: 4.5,
    review: 11,
    price: 240,
    img: "electronics.jpg",
    isBookmarked: true,
    isLiked: true,
    creatorCompany: "Company Name",
  },
  {
    ID: 7,
    name: "this is from H&K cat",
    brand: "H&K",
    cat: "h&k",
    // discount percentage
    discount: 10,
    rating: 4.5,
    review: 11,
    price: 240,
    img: "electronics.jpg",
    isBookmarked: true,
    isLiked: true,
    creatorCompany: "Company Name",
  },
  {
    ID: 8,
    name: "this is from C&T cat",
    brand: "C&T",
    cat: "c&t",
    // discount percentage
    discount: 10,
    rating: 4.5,
    review: 11,
    price: 240,
    img: "electronics.jpg",
    isBookmarked: true,
    isLiked: true,
    creatorCompany: "Company Name",
  },
  {
    ID: 9,
    name: "this is from C&T cat",
    brand: "C&T",
    cat: "c&t",
    // discount percentage
    discount: 10,
    rating: 4.5,
    review: 11,
    price: 240,
    img: "electronics.jpg",
    isBookmarked: true,
    isLiked: true,
    creatorCompany: "Company Name",
  },
  {
    ID: 10,
    name: "this is from C&T cat",
    brand: "C&T",
    cat: "c&t",
    // discount percentage
    discount: 10,
    rating: 4.5,
    review: 11,
    price: 240,
    img: "electronics.jpg",
    isBookmarked: true,
    isLiked: true,
    creatorCompany: "Company Name",
  },
  {
    ID: 11,
    name: "this is from H&B cat",
    brand: "H&B",
    cat: "h&b",
    // discount percentage
    discount: 10,
    rating: 4.5,
    review: 11,
    price: 240,
    img: "electronics.jpg",
    isBookmarked: true,
    isLiked: true,
    creatorCompany: "Company Name",
  },
  {
    ID: 12,
    name: "this is from H&B cat",
    brand: "H&B",
    cat: "h&b",
    // discount percentage
    discount: 10,
    rating: 4.5,
    review: 11,
    price: 240,
    img: "electronics.jpg",
    isBookmarked: true,
    isLiked: true,
    creatorCompany: "Company Name",
  },
  {
    ID: 13,
    name: "this is from H&B cat",
    brand: "H&B",
    cat: "h&b",
    // discount percentage
    discount: 10,
    rating: 4.5,
    review: 11,
    price: 240,
    img: "electronics.jpg",
    isBookmarked: true,
    isLiked: true,
    creatorCompany: "Company Name",
  },
  {
    ID: 14,
    name: "this is from f&c cat",
    brand: "f&c",
    cat: "f&c",
    // discount percentage
    discount: 10,
    rating: 4.5,
    review: 11,
    price: 240,
    img: "electronics.jpg",
    isBookmarked: true,
    isLiked: true,
    creatorCompany: "Company Name",
  },
  {
    ID: 15,
    name: "this is from f&c cat",
    brand: "f&c",
    cat: "f&c",
    // discount percentage
    discount: 10,
    rating: 4.5,
    review: 11,
    price: 240,
    img: "electronics.jpg",
    isBookmarked: true,
    isLiked: true,
    creatorCompany: "Company Name",
  },
  {
    ID: 16,
    name: "this is from f&c cat",
    brand: "f&c",
    cat: "f&c",
    // discount percentage
    discount: 10,
    rating: 4.5,
    review: 11,
    price: 240,
    img: "electronics.jpg",
    isBookmarked: true,
    isLiked: true,
    creatorCompany: "Company Name",
  },
  {
    ID: 17,
    name: "this is from b&s cat",
    brand: "b&s",
    cat: "b&s",
    // discount percentage
    discount: 10,
    rating: 4.5,
    review: 11,
    price: 240,
    img: "electronics.jpg",
    isBookmarked: true,
    isLiked: true,
    creatorCompany: "Company Name",
  },
  {
    ID: 18,
    name: "this is from b&s cat",
    brand: "b&s",
    cat: "b&s",
    // discount percentage
    discount: 10,
    rating: 4.5,
    review: 11,
    price: 240,
    img: "electronics.jpg",
    isBookmarked: true,
    isLiked: true,
    creatorCompany: "Company Name",
  },
]);

provide("products", products);
</script>
