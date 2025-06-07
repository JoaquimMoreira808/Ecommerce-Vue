<template>
  <nav class="bg-[#f0eeee] px-6 py-4 text-sm text-black shadow-md">
    <div class="max-w-7xl mx-auto flex justify-between items-center">

      <h1 class="text-5xl text-[#8c122f] font-bold tracking-wide" style="font-family: 'Playfair Display', serif;">
        Sacy's
      </h1>

      <ul class="flex text-1xl space-x-6 text-gray-700">
        <li>
          <router-link to="/" class="hover:text-[#8c122f] hover:scale-105 transition duration-200">
            Home
          </router-link>
        </li>
        <li><a href="#" class="hover:text-[#8c122f] hover:scale-105 transition duration-200">Products</a></li>
        <li class="relative">
          <DropdownCategoriesComponent />
        </li>
      </ul>

      <div class="flex space-x-4 text-lg">
        <a href="#" class="hover:text-[#8c122f] hover:scale-125 transition duration-300">
          <i class="fas fa-search"></i>
        </a>
        <input
          type="text"
          placeholder="Search products..."
          class="px-3 py-1 text-sm rounded-md border border-gray-300 focus:outline-none focus:ring-2 focus:ring-[#8c122f]"
        />
        <router-link to="/cart" class="hover:text-[#8c122f] hover:scale-125 transition duration-300">
          <i class="fas fa-shopping-cart"></i>
        </router-link>
      </div>
    </div>
  </nav>
</template>
<script>
import DropdownCategoriesComponent from '../components/DropdownCategoriesComponent.vue'

export default {
  components: {
    DropdownCategoriesComponent,
  },
}
</script>
