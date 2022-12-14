<template>
  <header class="app-header">
    <nav :class="setMenuStyleAndToggleSearchAndMenuOff">
      <div class="container">
        <router-link :to="{ name: 'home' }" class="brand">Boundry</router-link>
        <Transition name="search-input">
          <input
            type="text"
            name="search"
            id="search-input"
            placeholder="find something..."
            v-model="searchValue"
            v-show="isSearchInputVisible"
            ref="searchInput"
            class="nav-search-input"
          />
        </Transition>
        <ul>
          <li>
            <Search class="nav-search" @click="toggleSearchInput" />
          </li>
          <li>
            <Category
              @click="toggleCategorySubmenu"
              class="category-submenu-btn nav-category"
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
                          <router-link :to="{ name: 'productsList' }">{{
                            subItem
                          }}</router-link>
                        </li>
                      </ul>
                    </li>
                  </ul>
                </div>
              </div>
            </transition>
          </li>
          <li>
            <router-link :to="{ name: 'cart' }"
              ><Cart class="nav-cart"
            /></router-link>
          </li>
          <li>
            <router-link :to="{ name: 'login' }"
              ><User class="nav-user"
            /></router-link>
          </li>
        </ul>
      </div>
    </nav>
  </header>
</template>

<script setup>
import { ref, computed, onMounted, watch } from "vue";
import { useRoute, useRouter } from "vue-router";
// Icons
import Search from "../icons/Search.vue";
import Category from "../icons/Category.vue";
import Cart from "../icons/Cart.vue";
import User from "../icons/User.vue";
import Electronics from "../icons/NavbarCategory/Electronics.vue";
import Kid from "../icons/NavbarCategory/Kid.vue";
import Home from "../icons/NavbarCategory/Home.vue";
import Car from "../icons/NavbarCategory/Car.vue";
import Health from "../icons/NavbarCategory/Health.vue";
import Fashion from "../icons/NavbarCategory/Fashion.vue";
import Book from "../icons/NavbarCategory/Book.vue";

const searchValue = ref("");

const isSearchInputVisible = ref(false);
const searchInput = ref(null);
function toggleSearchInput() {
  isSearchInputVisible.value = !isSearchInputVisible.value;
  if (isSearchInputVisible.value)
    setTimeout(() => {
      searchInput.value.focus();
    }, 100);
}

const props = defineProps(["forceToggle"]);
const emits = defineEmits(["onResetForceToggle"]);
function watchForForceToggle(val) {
  if (val) {
    isCategorySubmenuOpen.value = false;
    emits("onResetForceToggle", false);
  }
}
watch(props, (newVal) => {
  watchForForceToggle(newVal);
});

const router = useRouter();
router.afterEach(() => {
  isCategorySubmenuOpen.value = false;
});

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
  window.addEventListener("scroll", changeNavClass);
});
checkUserDevice();

const route = useRoute();
let screenScrollValue = ref(null);
function changeNavClass() {
  screenScrollValue.value = window.scrollY;
  isSearchInputVisible.value = false;
  isCategorySubmenuOpen.value = false;
}
const setMenuStyleAndToggleSearchAndMenuOff = computed(() => {
  if (screenScrollValue.value < 10 && route.path === "/") return "";
  else return "fade-in";
});
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
