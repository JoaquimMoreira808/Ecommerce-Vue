<template>
    <h1 class="text-3xl font-bold mb-6 text-[#8c122f]">Your Cart</h1>
  <div class="bg-gray-100 min-h-screen p-6 flex justify-center">
    <div class="w-full max-w-7xl">
      <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
        <div class="lg:col-span-2 space-y-4 bg-white p-6 rounded-lg shadow">
            <CardProductCartComponent/>
          
        
        </div>
        <div class="bg-white rounded-lg shadow p-6 h-fit">
          <h2 class="text-xl font-semibold mb-4">Order Summary</h2>

          <div class="flex justify-between mb-2">
            <span>Subtotal</span>
            <span class="font-semibold"></span>
          </div>

          <div class="border-t pt-4 flex justify-between text-lg font-bold">
            <span>Total</span>
            <span></span>
          </div>
          <button
            class="mt-6 w-full bg-black text-white py-3 rounded-lg font-semibold hover:bg-[#8c122f] transition"
          >
            Go to Checkout →
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import CardProductCartComponent from '../components/CardProductCartComponent.vue'

export default {
  name: 'CartView',
  components: {
    CardProductCartComponent,
  },
}
</script>