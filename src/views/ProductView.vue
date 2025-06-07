<template>
  <div class="flex p-8 min-h-screen bg-gray-100 gap-10">
    <div class="flex-shrink-0 w-1/2 mr-8">
      <img
        v-if="product && product.images && product.images.length"
        :src="product.images[0]"
        :alt="product.title"
        class="w-full h-auto rounded shadow-lg object-cover"
      />
      <div
        v-else
        class="bg-gray-300 w-full h-96 flex items-center justify-center text-gray-500 rounded"
      >
        No image
      </div>
    </div>

    <div class="flex flex-col justify-start w-1/2">
      <h1 class="text-4xl font-bold mb-2 text-[#8c122f]">{{ product?.title || 'Carregando...' }}</h1>

      <div class="flex items-center gap-4 mb-4">
        <div class="flex items-center text-yellow-400">
          <svg
            v-for="n in 5"
            :key="n"
            class="w-5 h-5"
            :class="n <= Math.round(product?.rating) ? 'fill-current' : 'stroke-current'"
            xmlns="http://www.w3.org/2000/svg"
            viewBox="0 0 24 24"
            fill="none"
            stroke="currentColor"
            stroke-width="2"
            stroke-linecap="round"
            stroke-linejoin="round"
          >
            <polygon points="12 2 15 9 22 9 17 14 19 21 12 17 5 21 7 14 2 9 9 9 12 2"></polygon>
          </svg>
          <span class="ml-2 text-gray-700 font-semibold">{{ product?.rating.toFixed(1) || '0' }}</span>
        </div>
        <span class="text-gray-500">| {{ product?.stock }} em estoque</span>
        <span class="px-2 py-1 text-xs bg-green-200 text-green-800 rounded">
          {{ product?.category }}
        </span>
      </div>

      <p class="mb-6 text-gray-700 leading-relaxed">{{ product?.description }}</p>

      <div class="flex items-center gap-4 mb-6">
        <p class="text-3xl font-semibold text-black">
          R$ {{ formattedPrice }}
        </p>
        <p v-if="product.discountPercentage" class="text-red-600 line-through text-lg">
          R$ {{ product.price.toFixed(2) }}
        </p>
        <p
          v-if="product.discountPercentage"
          class="bg-red-600 text-white text-sm px-2 py-1 rounded"
        >
          -{{ product.discountPercentage.toFixed(0) }}%
        </p>
      </div>

      <button
        @click="addToCart"
        class="bg-[#8c122f] hover:bg-[#470b19] text-white py-3 rounded text-lg font-semibold w-48 transition-shadow shadow-md hover:shadow-lg"
        :disabled="!product"
      >
        Add to cart
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
  computed: {
    formattedPrice() {
      if (!this.product) return "0.00";
      const discount = this.product.discountPercentage || 0;
      const discountedPrice = this.product.price * (1 - discount / 100);
      return discountedPrice.toFixed(2);
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
    addToCart() {
      const productToCart = {
        id: this.product.id,
        title: this.product.title,
        price: this.formattedPrice,
        image: this.product.images[0] || '',
        quantity: 1,
      };

      const cart = JSON.parse(localStorage.getItem('cart')) || [];
      const existing = cart.find(p => p.id === productToCart.id);
      if (existing) {
        existing.quantity++;
      } else {
        cart.push(productToCart);
      }
      localStorage.setItem('cart', JSON.stringify(cart));
      alert(`${this.product.title} added to the cart.`);
    },
  },
};
</script>

<style scoped>
/* Só um ajuste no SVG das estrelas pra ficar bonitão */
svg.fill-current polygon {
  fill: #facc15; /* amarelo */
}
svg.stroke-current polygon {
  fill: none;
  stroke: #ccc;
}
</style>
