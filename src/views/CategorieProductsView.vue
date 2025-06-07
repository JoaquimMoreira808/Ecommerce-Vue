<template>
  <div class="p-6">
    <h1 class="text-3xl font-bold mb-6 text-[#8c122f]">
      Products in "{{ category }}"
    </h1>

    <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-6">
      <ProductCard
        v-for="product in pagedProducts"
        :key="product.id"
        :id="product.id"
        :title="product.title"
        :price="product.price"
        :description="product.description"
        :image="product.thumbnail"
        @select="viewProduct"
      />
    </div>

    <!-- Paginação -->
    <div class="mt-6 flex justify-center space-x-3">
      <button
        @click="prevPage"
        :disabled="currentPage === 1"
        class="px-4 py-2 rounded bg-[#8c122f] text-white disabled:opacity-50 hover:bg-[#700f28] transition"
      >
        ← Prev
      </button>

      <span class="flex items-center font-semibold">
        Page {{ currentPage }} of {{ totalPages }}
      </span>

      <button
        @click="nextPage"
        :disabled="currentPage === totalPages"
        class="px-4 py-2 rounded bg-[#8c122f] text-white disabled:opacity-50 hover:bg-[#700f28] transition"
      >
        Next →
      </button>
    </div>
  </div>
</template>

<script>
import ProductCard from '../components/ProductCardComponent.vue';

export default {
  name: 'CategorieProductsView',
  components: { ProductCard },
  props: {
    category: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      products: [],
      currentPage: 1,
      pageSize: 12,
    };
  },
  computed: {
    filteredProducts() {
      return this.products.filter(p => p.category === this.category);
    },
    totalPages() {
      return Math.ceil(this.filteredProducts.length / this.pageSize) || 1;
    },
    pagedProducts() {
      const start = (this.currentPage - 1) * this.pageSize;
      return this.filteredProducts.slice(start, start + this.pageSize);
    },
  },
  async created() {
    try {
      const res = await fetch('https://dummyjson.com/products?limit=1000');
      const data = await res.json();
      this.products = data.products;
    } catch (err) {
      console.error('Erro ao carregar produtos:', err);
    }
  },
  methods: {
    viewProduct(productId) {
      this.$router.push({ name: 'product', params: { id: productId.toString() } });
    },
    prevPage() {
      if (this.currentPage > 1) this.currentPage--;
    },
    nextPage() {
      if (this.currentPage < this.totalPages) this.currentPage++;
    },
  },
};
</script>
