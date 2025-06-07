<template>
  <div class="flex gap-4 items-center border-b py-4">
    <img :src="image" alt="Product Image" class="w-24 h-24 object-cover rounded" />
    <div class="flex-1">
      <h3 class="font-semibold text-lg">{{ title }}</h3>
      <p class="text-gray-600 flex items-center gap-3 mt-1">
        Quantity: 
        <button 
          @click="removeOne" 
          class="w-8 h-8 flex justify-center items-center rounded-md border border-gray-300 text-gray-600 hover:bg-gray-200 transition"
          aria-label="Decrease quantity"
        >−</button>
        <span class="px-3 font-medium text-gray-800">{{ localQuantity }}</span>
        <button 
          @click="addOne" 
          class="w-8 h-8 flex justify-center items-center rounded-md border border-gray-300 text-gray-600 hover:bg-gray-200 transition"
          aria-label="Increase quantity"
        >+</button>
      </p>
      <p class="text-gray-800 font-bold mt-2">US$ {{ (price * localQuantity).toFixed(2) }}</p>
      <button @click="removeFromCart" class="text-red-500 mt-3 hover:underline font-semibold">
        Remover
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CardProductCartComponent',
  props: {
    id: { type: [Number, String], required: true },
    title: { type: String, required: true },
    price: { type: Number, required: true },
    image: { type: String, default: '' },
    quantity: { type: Number, required: true },
  },
  data() {
    return {
      localQuantity: this.quantity,
    };
  },
  watch: {
    quantity(newVal) {
      this.localQuantity = newVal;
    },
  },
  methods: {
    updateCartQuantity(newQty) {
      if (newQty < 0) return; // evita quantidade negativa
      this.localQuantity = newQty;
      this.$emit('update-quantity', this.id, newQty);
    },

    addOne() {
      this.updateCartQuantity(this.localQuantity + 1);
    },

    removeOne() {
      if (this.localQuantity === 1) {
        if (confirm('Sure to remove from cart?')) {
          this.updateCartQuantity(0);
        }
      } else {
        this.updateCartQuantity(this.localQuantity - 1);
      }
    },

    removeFromCart() {
      if (confirm('Sure to remove from cart?')) {
        this.updateCartQuantity(0);
      }
    },
  },
};
</script>
