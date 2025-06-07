<template>
  <div
    class="w-64 bg-[#fafafa] border border-gray-200 rounded-2xl shadow-sm p-5 hover:shadow-md hover:-translate-y-1 transition-all duration-300 flex flex-col">
    <img :src="image" :alt="title" class="w-full h-40 object-cover rounded-xl mb-4 border border-gray-100" />
    <h3 class="text-lg font-semibold mb-1 text-gray-900">{{ title }}</h3>
    <p class="text-yellow-[#D4AF37] font-bold mb-2 text-base">R$ {{ price }}</p>
    <p class="text-gray-500 text-sm flex-grow leading-snug">{{ shortDescription }}</p>
    <button @click="addToCartClick"
      class="mt-4 bg-[#8c122f] hover:bg-[#470b19] text-white py-2 rounded-lg font-semibold shadow-md hover:shadow-lg transition-all duration-300">
      Add to cart
    </button>
    <button @click="viewMore"
      class="mt-4 bg-gray-700 hover:bg-black text-white py-2 rounded-lg font-semibold shadow-md hover:shadow-lg transition-all duration-300">
      Details
    </button>
  </div>
</template>

<script>
export default {
  name: 'ProductCard',
  inject: ['addToCart'],

  props: {
    id: { type: [Number, String], required: true },  // adicionei o id
    title: { type: String, required: true },
    price: { type: Number, required: true },
    description: { type: String, default: '' },
    image: { type: String, default: '' },
  },
  computed: {
    shortDescription() {
      return this.description.length > 60
        ? this.description.slice(0, 60) + '...'
        : this.description;
    },
  },
  methods: {
    addToCartClick() {
      const product = {
        id: this.id,
        title: this.title,
        price: this.price,
        image: this.image,
      };
      this.addToCart(product);
      alert(`Adicionado ${this.title} ao carrinho!`);
    },
    viewMore() {
      this.$emit('select', this.id);
    },
  },
};
</script>
