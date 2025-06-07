<template>
  <div class="relative">
   
    <button
      @click="toggle"
      class="text-gray-700 hover:text-[#8c122f] transition duration-200"
    >
      Categories ▼
    </button>

    
    <div
      v-if="show"
      class="absolute right-0 mt-2 w-56 origin-top-left divide-y divide-gray-100 rounded-md bg-white shadow-lg ring-1 ring-black/5 z-50"
    >
      <div class="py-1">
        <a href="#" class="block px-4 py-2 text-sm text-gray-700 hover:bg-gray-100"></a>
        <a href="#" class="block px-4 py-2 text-sm text-gray-700 hover:bg-gray-100">Duplicate</a>
      </div>
      <div class="py-1">
        <a href="#" class="block px-4 py-2 text-sm text-gray-700 hover:bg-gray-100">Archive</a>
        <a href="#" class="block px-4 py-2 text-sm text-gray-700 hover:bg-gray-100">Move</a>
      </div>
      <div class="py-1">
        <a href="#" class="block px-4 py-2 text-sm text-gray-700 hover:bg-gray-100">Share</a>
        <a href="#" class="block px-4 py-2 text-sm text-gray-700 hover:bg-gray-100">Add to favorites</a>
      </div>
    </div>
  </div>
</template>

<script>
export default {
//script para ocultar e mostrar o dropdown de categorias
  name: 'DropdownCategoriesComponent',
  data() {
    return {
      show: false,
    }
  },
  methods: {
    toggle() {
      this.show = !this.show
    },
  },
}
</script>

<style scoped>
</style>
