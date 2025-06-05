<script setup>
import NavbarComponent from "./components/NavbarComponent.vue";
import FooterComponent from "./components/FooterComponent.vue";
</script>

<template>
  <div class="app-container flex flex-col min-h-screen bg-[#f0eeee] text-black">
    
    <NavbarComponent />

    <main class="flex-grow px-6 py-8 max-w-7xl mx-auto">
      <router-view></router-view>
    </main>

    <FooterComponent />
  </div>
</template>
