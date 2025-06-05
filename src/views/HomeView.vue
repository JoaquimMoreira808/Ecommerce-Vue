<template>
  <div class="p-6 bg-gray-100 min-h-screen">

    <div class="flex flex-wrap gap-6 justify-center mb-6">
      <ProductCard
        v-for="product in products"
        :key="product.id"
        :id="product.id"
        :title="product.title"
        :price="product.price"
        :description="product.description"
        :image="product.thumbnail"
        @select="goToProduct"
      />
    </div>

    <!-- Pagination -->
    <div class="flex justify-center space-x-5">
      <button
        class="px-4 py-2 bg-teal-600 text-white rounded disabled:opacity-50"
        :disabled="currentPage === 1"
        @click="prevPage"
      >
        Previous
      </button>

      <span class="flex items-center font-semibold">
        Page {{ currentPage }} / {{ totalPages }}
      </span>

      <button
        class="px-4 py-2 bg-teal-600 text-white rounded disabled:opacity-50"
        :disabled="currentPage === totalPages"
        @click="nextPage"
      >
        Next
      </button>
    </div>

  </div>
</template>

<script>
import ProductCard from '../components/ProductCardComponent.vue'

export default {
  components: { ProductCard },

  data() {
    return {
      products: [],
      totalProducts: 0,
      currentPage: 1,
      pageSize: 5,
    };
  },

  computed: {
    totalPages() {
      return Math.ceil(this.totalProducts / this.pageSize);
    },
  },

  methods: {
    fetchProducts() {
      const skip = (this.currentPage - 1) * this.pageSize;
      fetch(`https://dummyjson.com/products?limit=${this.pageSize}&skip=${skip}`)
        .then(res => res.json())
        .then(data => {
          this.products = data.products;
          this.totalProducts = data.total;
        });
    },
    nextPage() {
      if (this.currentPage < this.totalPages) {
        this.currentPage++;
        this.fetchProducts();
      }
    },
    prevPage() {
      if (this.currentPage > 1) {
        this.currentPage--;
        this.fetchProducts();
      }
    },
    goToProduct(id) {
      this.$router.push({ name: 'product', params: { id: id.toString() } });
    },
  },

  mounted() {
    this.fetchProducts();
  },
};
</script>
