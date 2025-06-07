<template>
  <div class="bg-gray-100 min-h-screen p-6 flex justify-center">
    <div class="w-full max-w-7xl">
      <h1 class="text-3xl font-bold mb-6 text-[#8c122f]">Your Cart</h1>
      <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
        <div class="lg:col-span-2 space-y-4 bg-white p-6 rounded-lg shadow">
          <CardProductCartComponent
            v-for="item in cart"
            :key="item.id"
            :id="item.id"
            :title="item.title"
            :price="item.price"
            :image="item.image"
            :quantity="item.quantity"
            @remove="removeFromCart"
            @update-quantity="updateQuantity"
          />
          <p v-if="cart.length === 0" class="text-center text-gray-500 mt-4">
            Seu carrinho está vazio.
          </p>
        </div>
        <div class="bg-white rounded-lg shadow p-6 h-fit">
          <h2 class="text-xl font-semibold mb-4">Order Summary</h2>
          <div class="flex justify-between mb-2">
            <span>Subtotal</span>
            <span class="font-semibold">US$ {{ subtotal.toFixed(2) }}</span>
          </div>
          <div class="border-t pt-4 flex justify-between text-lg font-bold">
            <span>Total</span>
            <span>US$ {{ subtotal.toFixed(2) }}</span>
          </div>
          <button
            class="mt-6 w-full bg-black text-white py-3 rounded-lg font-semibold hover:bg-[#8c122f] transition"
            :disabled="cart.length === 0"
          >
            Go to Checkout →
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, computed, onMounted } from 'vue';
import CardProductCartComponent from '../components/CardProductCartComponent.vue';

export default {
  name: 'CartView',
  components: { CardProductCartComponent },

  setup() {
    const cart = ref([]);

    function loadCart() {
      cart.value = JSON.parse(localStorage.getItem('cart')) || [];
    }

    function removeFromCart(id) {
      cart.value = cart.value.filter(item => item.id !== id);
      localStorage.setItem('cart', JSON.stringify(cart.value));
    }

    function updateQuantity(id, newQty) {
      const index = cart.value.findIndex(item => item.id === id);
      if (index !== -1) {
        if (newQty <= 0) {
          cart.value.splice(index, 1);
        } else {
          cart.value[index].quantity = newQty;
        }
        localStorage.setItem('cart', JSON.stringify(cart.value));
      }
    }

    onMounted(() => {
      loadCart();
    });

    const subtotal = computed(() =>
      cart.value.reduce((sum, item) => sum + item.price * item.quantity, 0)
    );

    return { cart, removeFromCart, updateQuantity, subtotal };
  },
};
</script>
