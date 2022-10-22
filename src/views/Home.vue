<template>
  <the-navigation></the-navigation>
  <section class="subheader container">
    <article v-for="item in subheaderItems">
      <img :src="item.imgUrl" :alt="item.title" />
      <h4>{{ item.title }}</h4>
      <p>{{ item.subtitle }}</p>
    </article>
  </section>
</template>

<script setup>
import TheNavigation from "../components/layout/TheNavigation.vue";
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
</script>
