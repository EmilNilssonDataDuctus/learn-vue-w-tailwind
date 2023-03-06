<template>
  <main class="container text-white">
    <h1>Hello world</h1>
    <div class="relative pt-4 mb-8">
      <input
        v-model="searchQuery"
        @input="getSearchResults"
        type="text"
        name=""
        id=""
        placeholder="Search for city of state"
        class="input"
      />
      <div
        v-if="mapboxSearchResults"
        class="absolute bg-weather-secondary text-white w-full shadow-md py-2 px-1 top-[66px]"
      >
        <p v-if="searchError">Something went wrong, try again</p>
        <p v-if="!searchError && mapboxSearchResults.length === 0">
          No results, try again
        </p>
        <template v-else>
          <ul>
            <li
              v-for="searchResult in mapboxSearchResults"
              :key="searchResult.id"
              class="py-2 cursor-pointer"
              @click="previewCity(searchResult)"
            >
              {{ searchResult.place_name }}
            </li>
          </ul>
        </template>
      </div>
    </div>
  </main>
</template>

<script setup>
import { ref } from "vue";
import axios from "axios";

const previewCity = (searchResult) => {
  console.log(searchResult);
};

const searchQuery = ref("");
const queryTimeout = ref(null);
const mapboxSearchResults = ref(null);
const searchError = ref(null);

const getSearchResults = () => {
  clearTimeout(queryTimeout.value);

  queryTimeout.value = setTimeout(async () => {
    if (searchQuery.value !== "") {
      try {
        // const result = await axios.get(``);
        // mapboxSearchResults.value = result.data.features;
        // console.log(mapboxSearchResults.value);
      } catch {
        searchError.value = true;
      }
      mapboxSearchResults.value = [];
      return;
    }
    mapboxSearchResults.value = null;
  }, 300);
};
</script>
