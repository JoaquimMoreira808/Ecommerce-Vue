<template>
  <div class="p-6 bg-gray-100 min-h-screen space-y-12">

    <section class="max-w-5xl mx-auto text-center">
      <h2 class="text-4xl font-bold text-[#8c122f] mb-4">About Sacy's</h2>
      <p class="text-lg text-gray-700 leading-relaxed">
        Welcome to <strong>Sacy's</strong> – your one-stop shop for everything from elegant fragrances to the latest smartphones. We curate the best products to elevate your everyday life.
        Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla quis lorem ut libero malesuada feugiat. Vivamus magna justo, lacinia eget consectetur sed, convallis at tellus.
      </p>
    </section>

    <section v-for="(section, index) in productSections" :key="index" class="max-w-7xl mx-auto">
      <h3 class="text-2xl font-semibold text-gray-800 mb-4">{{ section.title }}</h3>
      <div class="flex gap-4 overflow-x-auto pb-4">
        <ProductCard
          v-for="product in section.products"
          :key="product.id"
          :id="product.id"
          :title="product.title"
          :price="product.price"
          :description="product.description"
          :image="product.images[0]"
          @select="goToProduct"
        />
      </div>
    </section>

  </div>
</template>

<script>
import ProductCard from '../components/ProductCardComponent.vue';

export default {
  components: { ProductCard },

  data() {
    return {
      currentPage: 1,
      pageSize: 6,
      productSections: [],
    };
  },

  computed: {
    totalPages() {
      return Math.ceil(30 / this.pageSize);
    }
  },

  methods: {
    async fetchSection(category, title) {
      const res = await fetch(`https://dummyjson.com/products/category/${category}`);
      const data = await res.json();
      this.productSections.push({ title, products: data.products.slice(0, 6) });
    },


    goToProduct(id) {
      this.$router.push({ name: 'product', params: { id: id.toString() } });
    }
  },

  async mounted() {
    await this.fetchSection('smartphones', 'Latest Smartphones');
    await this.fetchSection('fragrances', 'Elegant Fragrances');
  }
};
</script>
