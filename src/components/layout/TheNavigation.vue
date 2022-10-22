<template>
  <header>
    <nav>
      <div class="container">
        <router-link to="/" class="brand">Boundry</router-link>
        <Transition name="search-input">
          <input
            type="text"
            name="search"
            id="search-input"
            placeholder="find something..."
            v-model="searchValue"
            v-show="isSearchInputVisible"
            ref="searchInput"
          />
        </Transition>
        <ul>
          <li><Search @click="toggleSearchInput" /></li>
          <li>
            <Category
              @click="toggleCategorySubmenu"
              class="category-submenu-btn"
            />
            <transition name="dropdown-category-submenu">
              <div
                class="category-submenu-desktop"
                v-if="isCategorySubmenuOpen && !isOnMobile"
              >
                <div class="container">
                  <ul class="categories-list">
                    <li>
                      <button
                        :class="{
                          active: currentSubmenuCategory === 'electronic',
                        }"
                        @click="setCurrentSubmenuCategory('electronic')"
                      >
                        <Electronics />
                        <span>Electronics</span>
                      </button>
                    </li>
                    <li>
                      <button
                        :class="{
                          active: currentSubmenuCategory === 'home',
                        }"
                        @click="setCurrentSubmenuCategory('home')"
                      >
                        <Home />
                        <span>Home & Kitchen</span>
                      </button>
                    </li>
                    <li>
                      <button
                        :class="{
                          active: currentSubmenuCategory === 'car',
                        }"
                        @click="setCurrentSubmenuCategory('car')"
                      >
                        <Car />
                        <span>Car & Tools</span>
                      </button>
                    </li>
                    <li>
                      <button
                        :class="{
                          active: currentSubmenuCategory === 'health',
                        }"
                        @click="setCurrentSubmenuCategory('health')"
                      >
                        <Health />
                        <span>Health & Beauty</span>
                      </button>
                    </li>
                    <li>
                      <button
                        :class="{
                          active: currentSubmenuCategory === 'fashion',
                        }"
                        @click="setCurrentSubmenuCategory('fashion')"
                      >
                        <Fashion />
                        <span>Fashion & Clothing</span>
                      </button>
                    </li>
                    <li>
                      <button
                        :class="{
                          active: currentSubmenuCategory === 'book',
                        }"
                        @click="setCurrentSubmenuCategory('book')"
                      >
                        <Book />
                        <span>Books & Stationary</span>
                      </button>
                    </li>
                    <li>
                      <button
                        :class="{
                          active: currentSubmenuCategory === 'kid',
                        }"
                        @click="setCurrentSubmenuCategory('kid')"
                      >
                        <Kid />
                        <span>Kids & Babes</span>
                      </button>
                    </li>
                  </ul>
                  <ul class="brands-list">
                    <li
                      class="brands-item"
                      v-for="item in categoryDropdownSubmenu"
                    >
                      <h4>{{ item.title }}</h4>
                      <ul class="brand-list">
                        <li
                          class="brand-list-item"
                          v-for="subItem in item.subItems"
                        >
                          <router-link to="/">{{ subItem }}</router-link>
                        </li>
                      </ul>
                    </li>
                  </ul>
                </div>
              </div>
            </transition>
          </li>
          <li><Cart /></li>
          <li><User /></li>
        </ul>
      </div>
    </nav>
    <form
      class="header-overlay"
      autocomplete="off"
      @click="isCategorySubmenuOpen = false"
    >
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
    <Transition name="category-submenu">
      <section
        class="category-submenu-mobile"
        v-if="isCategorySubmenuOpen && isOnMobile"
      >
        <h4>Category:</h4>
        <Close class="close-btn" @click="toggleCategorySubmenu" />
        <article>
          <router-link to="/" class="electronics">
            <Electronics />
            <p>Electronics</p>
          </router-link>
          <router-link to="/" class="electronics">
            <Home />
            <p>Home & Kitchen</p>
          </router-link>
          <router-link to="/" class="electronics">
            <Car />
            <p>Car & Tools</p>
          </router-link>
          <router-link to="/" class="electronics">
            <Health />
            <p>Health & Beauty</p>
          </router-link>
          <router-link to="/" class="electronics">
            <Fashion />
            <p>Fashion & Clothing</p>
          </router-link>
          <router-link to="/" class="electronics">
            <Book />
            <p>Books & Stationary</p>
          </router-link>
          <router-link to="/" class="electronics">
            <Kid />
            <p>Kids & Babes</p>
          </router-link>
        </article>
      </section>
    </Transition>
  </header>
</template>

<script setup>
import { ref, computed, onMounted } from "vue";
// Icons
import Search from "../icons/Search.vue";
import Category from "../icons/Category.vue";
import Cart from "../icons/Cart.vue";
import User from "../icons/User.vue";
import Close from "../icons/Close.vue";
import Electronics from "../icons/NavbarCategory/Electronics.vue";
import Kid from "../icons/NavbarCategory/Kid.vue";
import Home from "../icons/NavbarCategory/Home.vue";
import Car from "../icons/NavbarCategory/Car.vue";
import Health from "../icons/NavbarCategory/Health.vue";
import Fashion from "../icons/NavbarCategory/Fashion.vue";
import Book from "../icons/NavbarCategory/Book.vue";

const searchValue = ref("");
const setSearchInputStyle = computed(() =>
  searchValue.value.trim() !== "" ? "bg-white" : ""
);

const isSearchInputVisible = ref(false);
const searchInput = ref(null);
function toggleSearchInput() {
  isSearchInputVisible.value = !isSearchInputVisible.value;
  if (isSearchInputVisible.value)
    setTimeout(() => {
      searchInput.value.focus();
    }, 100);
}
const isCategorySubmenuOpen = ref(false);
function toggleCategorySubmenu() {
  isCategorySubmenuOpen.value = !isCategorySubmenuOpen.value;
}
const currentSubmenuCategory = ref("electronic");
function setCurrentSubmenuCategory(name) {
  currentSubmenuCategory.value = name;
}

const isOnMobile = ref(null);
function checkUserDevice() {
  window.innerWidth > 768
    ? (isOnMobile.value = false)
    : (isOnMobile.value = true);
}
onMounted(() => {
  window.addEventListener("resize", checkUserDevice);
});
checkUserDevice();

const categoryDropdownSubmenu = ref([
  {
    title: "PC",
    subItems: [
      "CPU",
      "Graphic Card",
      "Main Board",
      "RAM",
      "Case",
      "SSD",
      "HDD",
    ],
  },
  {
    title: "Mobile",
    subItems: [
      "Apple",
      "Samsung",
      "Xiaomi",
      "Oppo",
      "Vivo",
      "Asus",
      "Google",
      "Sony",
    ],
  },
  {
    title: "Laptop",
    subItems: ["Asus", "MSI", "Gigabyte", "Xiaomi", "Acer", "Apple", "Google"],
  },
  {
    title: "Accessories",
    subItems: [
      "Cables",
      "Power Strip",
      "Surge Protector",
      "Bag Smart",
      "Others",
    ],
  },
]);
</script>
