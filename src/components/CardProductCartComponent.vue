<template>
  <div class="flex-1 space-y-4">
    <div class="flex items-center justify-between bg-white rounded-lg shadow p-4">
      <div class="flex items-center space-x-4">
        <img src="" alt="Product" class="w-20 h-20 object-cover rounded" />
        <div>
          <h2 class="font-semibold">Name</h2>
          <p class="font-bold mt-2">R$</p>
        </div>
      </div>
    </div>
    <div class="flex items-center space-x-2">
      <button
        @click="decrement"
        class="px-3 py-1 bg-gray-200 rounded hover:bg-gray-300 transition"
        :disabled="quantity <= 1"
      >
        -
      </button>
      <span class="min-w-[24px] text-center font-semibold">{{ quantity }}</span>
      <button
        @click="increment"
        class="px-3 py-1 bg-gray-200 rounded hover:bg-gray-300 transition"
      >
        +
      </button>    
      <button class="text-red-500 ml-4 hover:text-red-700 transition">
        <i class="fas fa-trash"></i>
      </button>
    </div>
  </div>
</template>
<script>
//script para diminuir e aumentar a quantia dos items adicionados ao carrinho
export default {
  data() {
    return {
      quantity: 1,
    };
  },
  methods: {
    increment() {
      this.quantity++;
    },
    decrement() {
      if (this.quantity > 1) {
        this.quantity--;
      }
    },
  },
};
</script>

<style scoped>
</style>
