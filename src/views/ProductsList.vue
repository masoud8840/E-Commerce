<template>
  <article class="products-list-view">
    <div class="container">
      <transition name="products-filter">
        <article
          class="products-list-filter"
          :class="{ mobile: isMobileDevice }"
          v-if="isFilterOptionsMenuOpen || !isMobileDevice"
          @click="toggleOffOptionsMenu($event, 'article')"
        >
          <div>
            <button
              class="close-filter-list-btn"
              @click="onToggleOptionsMenu"
              v-if="isFilterOptionsMenuOpen && isMobileDevice"
            >
              <Close />
            </button>

            <section
              class="list-filter-cotegory"
              :class="{ active: categoryChoice.length > 0 }"
            >
              <h5>Category</h5>
              <ul>
                <li class="input-group" v-for="cat in categories">
                  <input
                    type="checkbox"
                    :id="cat"
                    :value="cat"
                    v-model="categoryChoice"
                    @input="onFilterInputChecked(cat)"
                  />
                  <label :for="cat">{{ cat }}</label>
                </li>
              </ul>
            </section>

            <section
              class="list-filter-brand"
              :class="{ active: brandChoice.length > 0 }"
            >
              <h5>Brands</h5>
              <ul>
                <li class="input-group input-text">
                  <input
                    type="text"
                    id="brand-search"
                    name="search"
                    placeholder="Search"
                    v-model="brandSearch"
                  />
                  <Search />
                </li>
                <li
                  class="input-group"
                  v-for="brand in showBrandsList"
                  :key="brand"
                >
                  <input
                    type="checkbox"
                    :id="brand"
                    :value="brand"
                    v-model="brandChoice"
                    @input="onFilterInputChecked(brand)"
                  />
                  <label :for="brand">{{ brand }}</label>
                </li>
              </ul>
            </section>

            <section
              class="list-filter-price"
              :class="{ active: +minPrice !== 0 || +maxPrice !== 3000 }"
            >
              <h5>Price</h5>
              <div class="price-container">
                <div class="progress" :style="priceProgressBarStyles"></div>
                <div class="inputs">
                  <input
                    type="range"
                    class="min-price"
                    min="0"
                    step="50"
                    max="3000"
                    v-model="minPrice"
                    @input="onInputPriceChange"
                  />
                  <input
                    type="range"
                    class="max-price"
                    min="0"
                    step="5"
                    max="3000"
                    v-model="maxPrice"
                    @input="onInputPriceChange"
                  />
                </div>
              </div>
              <div class="price-output">
                <span class="price-min">${{ minPrice }}</span>
                <div class="price-seprator">
                  <span>from</span>
                  <span>to</span>
                </div>
                <span class="price-max">${{ maxPrice }}</span>
              </div>
            </section>
          </div>
        </article>
      </transition>
      <article class="products-list-inner">
        <article class="breadcrumb">
          <div class="breadcrumb-inner">
            <span>Women</span>
            <img
              src="/public/images/ProductsList/BreadcrumbArrow.svg"
              alt="arrow-icon"
            />
            <span>Shoe</span>
          </div>
          <button @click="onToggleOptionsMenu">
            <Options
              class="options-btn"
              v-if="isMobileDevice && !isFilterOptionsMenuOpen"
            />
            <Close v-if="isMobileDevice && isFilterOptionsMenuOpen" />
          </button>
        </article>
        <article class="filtered-tags">
          <button
            class="filtered-tag"
            v-for="tag in filteredListTags"
            :key="tag"
            @click="onRemoveFilteredTags(tag)"
          >
            {{ tag }}
            <Close />
          </button>
        </article>
        <article class="product-list-list">
          <product-item></product-item>
        </article>
      </article>
    </div>
  </article>
</template>

<script setup>
import { ref, onMounted, watch, computed } from "vue";
import Options from "../components/icons/ProductsList/Options.vue";
import Close from "../components/icons/Close.vue";
import Search from "../components/icons/Search.vue";
import ProductItem from "../components/UI/ProductItem.vue";
const isMobileDevice = ref(false);
const isFilterOptionsMenuOpen = ref(false);

// check for mobile devices
onMounted(() => {
  window.addEventListener("resize", onResizeWindow);
});

function onResizeWindow() {
  if (window.innerWidth < 576) isMobileDevice.value = true;
  else isMobileDevice.value = false;
}
onResizeWindow();

function onToggleOptionsMenu() {
  isFilterOptionsMenuOpen.value = !isFilterOptionsMenuOpen.value;
}
function toggleOffOptionsMenu(e, srcEl) {
  if (e.target.localName !== srcEl) return;
  isFilterOptionsMenuOpen.value = false;
}

const filteredListTags = ref([]);

// Category list
const categories = ref([
  "soccer",
  "original",
  "training",
  "football",
  "basketball",
  "vallyball",
]);
const categoryChoice = ref([]);

const brands = ref(["nike", "adidas", "zara", "zengary", "detoly"]);
const brandChoice = ref([]);
const brandSearch = ref("");

const showBrandsList = computed(() => {
  if (brandSearch.value.trim() === "") return brands.value;
  else
    return brands.value.filter((brand) => {
      return brand.includes(brandSearch.value);
    });
});
watch(brandChoice, () => {
  brandSearch.value = "";
});

const minPrice = ref(0);
const maxPrice = ref(3000);

const priceChoice = ref("");

function onInputPriceChange(e) {
  // assign gap between min and max price
  const priceGap = +300;
  if (maxPrice.value - minPrice.value < priceGap) {
    if (e.target.className === "min-price")
      minPrice.value = +maxPrice.value - +priceGap;
    else maxPrice.value = +minPrice.value + +priceGap;
  }

  // Find price filter
  const priceFilterTagIndex = filteredListTags.value.findIndex((tag) =>
    tag.includes("$")
  );
  // if price filter isn't exist, add
  if (priceFilterTagIndex == -1) {
    priceChoice.value = `$${minPrice.value} - $${maxPrice.value}`;
    filteredListTags.value.push(priceChoice.value);
  }
  // if price filter exist overwrite it's values
  else {
    filteredListTags.value[
      priceFilterTagIndex
    ] = `$${minPrice.value} - $${maxPrice.value}`;
  }

  // delete price filter if default values
  if (+minPrice.value === 0 && +maxPrice.value === 3000) {
    filteredListTags.value.splice(priceFilterTagIndex, 1);
  }
}
function onRemoveFilteredTags(tagName) {
  const indexInBrandChoice = brandChoice.value.findIndex(
    (brand) => brand === tagName
  );
  const indexInCategoryChoice = categoryChoice.value.findIndex(
    (cat) => cat === tagName
  );
  if (indexInBrandChoice > -1) {
    brandChoice.value.splice(indexInBrandChoice, 1);
    filteredListTags.value = filteredListTags.value.filter(
      (tag) => tag !== tagName
    );
  } else if (indexInCategoryChoice > -1) {
    categoryChoice.value.splice(indexInCategoryChoice, 1);
    filteredListTags.value = filteredListTags.value.filter(
      (tag) => tag !== tagName
    );
  } else if (tagName.includes("$")) {
    const priceFilterTagIndex = filteredListTags.value.findIndex((tag) =>
      tag.includes("$")
    );
    minPrice.value = 0;
    maxPrice.value = 3000;
    filteredListTags.value.splice(priceFilterTagIndex, 1);
  }
}

function onFilterInputChecked(input) {
  const findedIndex = filteredListTags.value.findIndex((tag) => tag === input);
  if (findedIndex === -1) {
    filteredListTags.value.push(input);
  } else {
    filteredListTags.value.splice(findedIndex, 1);
  }
}
const priceProgressBarStyles = computed(() => {
  // let maxValue = +minPriceSlider.value.max;
  // 3000 is the max price range slider
  return {
    left: `${(minPrice.value / 3000) * 100}%`,
    right: `${100 - (maxPrice.value / 3000) * 100}%`,
  };
});
</script>
