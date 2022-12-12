<template>
  <the-navigation
    :force-toggle="toggleOff"
    @on-reset-force-toggle="resetForceToggle"
  ></the-navigation>
  <router-view @click="forceToggleOffNav"></router-view>
</template>

<script setup>
import { ref } from "vue";
import TheNavigation from "./components/layout/TheNavigation.vue";

const toggleOff = ref(false);
function forceToggleOffNav() {
  toggleOff.value = true;
}

function resetForceToggle(forceToggleValue) {
  toggleOff.value = forceToggleValue;
}
</script>
