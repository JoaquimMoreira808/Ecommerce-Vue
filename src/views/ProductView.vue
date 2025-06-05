<template>
  <div class="flex p-8 min-h-screen bg-gray-100">
    <div class="flex-shrink-0 w-1/2 mr-8">
      <img
        v-if="product && product.images.length"
        :src="product.images[0]"
        :alt="product.title"
        class="w-full h-auto rounded shadow-lg"
      />
      <div v-else class="bg-gray-300 w-full h-96 flex items-center justify-center text-gray-500">
        Sem imagem
      </div>
    </div>

    <!-- Detalhes do produto à direita -->
    <div class="flex flex-col justify-start w-1/2">
      <h1 class="text-4xl font-bold mb-4">{{ product?.title || 'Carregando...' }}</h1>
      <p class="mb-6 text-gray-700">{{ product?.description }}</p>

      <p class="text-2xl font-semibold mb-6 text-teal-700">
        R$ {{ product?.price ? product.price.toFixed(2) : '0.00' }}
      </p>

      <button
        @click="buyProduct"
        class="bg-[#8c122f] hover:bg-[#470b19] text-white py-3 rounded text-lg font-semibold w-48"
        :disabled="!product"
      >
        Comprar
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "ProductView",
  props: {
    id: { type: String, required: true },
  },
  data() {
    return {
      product: null,
    };
  },
  watch: {
    id: {
      immediate: true,
      handler(newId) {
        this.fetchProduct(newId);
      },
    },
  },
  methods: {
    fetchProduct(id) {
      fetch(`https://dummyjson.com/products/${id}`)
        .then((res) => {
          if (!res.ok) throw new Error("Produto não encontrado");
          return res.json();
        })
        .then((data) => {
          this.product = data;
        })
        .catch(() => {
          this.product = null;
          this.$router.push("/404");
        });
    },
    buyProduct() {
      alert(`Você comprou: ${this.product.title}!`);
    },
  },
};
</script>

<style scoped>
/* Pode ajustar se quiser, mas o Tailwind já ajuda bastante */
</style>
