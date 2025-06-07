<template>
  <nav class="bg-[#f0eeee] px-6 py-4 text-sm text-black shadow-md">
    <div class="max-w-7xl mx-auto flex justify-between items-center">
      <h1
        class="text-5xl text-[#8c122f] font-bold tracking-wide"
        style="font-family: 'Playfair Display', serif;"
      >
        Sacy's
      </h1>
      <ul class="flex text-1xl space-x-6 text-gray-700">
        <li>
          <router-link
            to="/"
            class="hover:text-[#8c122f] hover:scale-105 transition duration-200"
          >
            Home
          </router-link>
        </li>
        <li class="relative">
          <DropdownCategoriesComponent />
        </li>
      </ul>

      <div class="relative w-64" ref="searchContainer">
        <input
          v-model="searchQuery"
          @input="onInput"
          @focus="isDropdownOpen = true"
          type="text"
          placeholder="Search products..."
          class="w-full px-4 py-2 text-sm rounded-md border border-gray-300 focus:outline-none focus:ring-2 focus:ring-[#8c122f] shadow-sm"
        />
        <ul
          v-if="isDropdownOpen && searchQuery && suggestions.length"
          class="absolute z-50 mt-1 w-full bg-white border border-gray-300 rounded-lg shadow-lg max-h-60 overflow-y-auto"
        >
          <li
            v-for="product in suggestions"
            :key="product.id"
            @click="selectSuggestion(product.id)"
            class="px-4 py-2 hover:bg-[#f6e9ec] cursor-pointer transition-colors"
          >
            {{ product.title }}
          </li>
        </ul>

        <div
          v-else-if="isDropdownOpen && searchQuery && !suggestions.length"
          class="absolute z-50 mt-1 w-full bg-white border border-gray-300 rounded-lg shadow px-4 py-2 text-gray-500 italic"
        >
          No results found.
        </div>
      </div>

      <div class="flex space-x-4 text-lg ml-4">
        <router-link
          to="/cart"
          class="hover:text-[#8c122f] hover:scale-125 transition duration-300"
        >
          <i class="fas fa-shopping-cart"></i>
        </router-link>
      </div>
    </div>
  </nav>
</template>

<script>
import DropdownCategoriesComponent from '../components/DropdownCategoriesComponent.vue';

export default {
  components: {
    DropdownCategoriesComponent,
  },
  data() {
    return {
      isDropdownOpen: false,
      suggestions: [],
      debounceTimeout: null,
      searchQuery: '',
    };
  },
  methods: {
    onInput() {
      clearTimeout(this.debounceTimeout);
      if (!this.searchQuery.trim()) {
        this.suggestions = [];
        this.isDropdownOpen = false;
        return;
      }

      this.debounceTimeout = setTimeout(() => {
        fetch(
          `https://dummyjson.com/products/search?q=${encodeURIComponent(
            this.searchQuery
          )}`
        )
          .then((res) => res.json())
          .then((data) => {
            this.suggestions = data.products;
            this.isDropdownOpen = true;
          });
      }, 400);
    },
    selectSuggestion(productId) {
      this.isDropdownOpen = false;
      this.suggestions = [];
      this.searchQuery = '';
      this.$router.push({ name: 'product', params: { id: productId.toString() } });
    },
    handleClickOutside(event) {
      const container = this.$refs.searchContainer;
      if (container && !container.contains(event.target)) {
        this.isDropdownOpen = false;
      }
    },
  },
  mounted() {
    document.addEventListener('click', this.handleClickOutside);
  },
  beforeUnmount() {
    document.removeEventListener('click', this.handleClickOutside);
  },
};
</script>