<template>
  <main class="container text-white">
    <h1>Hello world</h1>
    <div class="relative pt-4 mb-8">
      <input
        v-model="searchQuery"
        type="text"
        name=""
        id=""
        placeholder="Search for city of state"
        class="w-full px-1 py-2 bg-transparent border-b focus:border-weather-secondary focus:outline-none focus:shadow-[0px_1px_0_0_#004E71]"
      />
    </div>
  </main>
</template>

<script setup>
import { ref } from "vue";

const searchQuery = ref("");
</script>
