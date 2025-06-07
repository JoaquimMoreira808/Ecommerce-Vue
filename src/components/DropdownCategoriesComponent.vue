<template>
  <div class="relative" v-outside="() => show = false">
    <button
      @click="toggle"
      class="text-gray-700 hover:text-[#8c122f] transition duration-200 font-semibold"
    >
      Categories ▼
    </button>

    <div
      v-if="show"
      class="absolute right-0 mt-2 w-64 max-h-64 origin-top-left rounded-md bg-white shadow-lg ring-1 ring-black/5 z-50 overflow-y-auto"
    >
      <div class="py-1">
        <a
          v-for="(category, index) in categories"
          :key="category"
          href="#"
          @click.prevent="selectCategory(category)"
          class="block px-4 py-2 text-sm text-gray-700 hover:bg-[#f6e9ec] cursor-pointer"
        >
          {{ category }}
        </a>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'DropdownCategoriesComponent',
  data() {
    return {
      show: false,
      categories: [],
    };
  },
  methods: {
    toggle() {
      this.show = !this.show;
      if (this.show && this.categories.length === 0) {
        this.fetchCategories();
      }
    },
    async fetchCategories() {
      try {
        const res = await fetch('https://dummyjson.com/products?limit=1000');
        const data = await res.json();
        this.categories = [...new Set(data.products.map(p => p.category))];
      } catch (error) {
        console.error('Erro ao buscar categorias:', error);
      }
    },
    selectCategory(category) {
      this.show = false;
      this.$router.push({ name: 'category-products', params: { category } });
    },
  },
  directives: {
    outside: {
      beforeMount(el, binding) {
        el.clickOutsideEvent = event => {
          if (!(el === event.target || el.contains(event.target))) {
            binding.value(event);
          }
        };
        document.body.addEventListener('click', el.clickOutsideEvent);
      },
      unmounted(el) {
        document.body.removeEventListener('click', el.clickOutsideEvent);
      },
    },
  },
};
</script>
