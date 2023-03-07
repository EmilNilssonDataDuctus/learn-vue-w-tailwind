<template>
  <div class="flex flex-col items-center flex-1">
    <div
      v-if="route.query.preview"
      class="w-full p-4 text-center text-white bg-weather-secondary"
    >
      <p>You are previewing this city</p>
      <p>Click + to start tracking this city</p>
    </div>
    <div class="flex flex-col items-center py-12 text-white">
      <h1 class="mb-2 text-4xl">{{ route.params.city }}</h1>
      <p>Current temp: {{ convertToCelcius(weatherData.main.temp) }}&deg;</p>
      <p>
        Feels like:
        {{ Math.round(convertToCelcius(weatherData.main["feels_like"])) }}&deg;
      </p>
      <p class="capitalize">
        {{ weatherData.weather[0].description }}
      </p>
      <img
        class="w-[150px]"
        :src="`http://openweathermap.org/img/wn/${weatherData.weather[0].icon}@2x.png`"
      />
      <h2 class="self-start">Formatted data</h2>
      <pre>
        {{ JSON.stringify(weatherData, null, 2) }}
      </pre>
    </div>
  </div>
</template>

<script setup>
import axios from "axios";
import { useRoute } from "vue-router";

const route = useRoute();
const openWeatherAPIKey = import.meta.env.VITE_APP_OPENWEATHER_API;

const convertToCelcius = (tempInKelvin) => tempInKelvin - 271;
const getWeatherData = async () => {
  try {
    const weatherData = await axios.get(
      `https://api.openweathermap.org/data/2.5/weather?lat=${route.query.lat}&lon=${route.query.lng}&appid=${openWeatherAPIKey}`
    );
    console.log("weatherData.data");
    console.log(weatherData.data);
    console.log("weatherData");
    console.log(weatherData);

    return weatherData.data;
  } catch (error) {}
};
const weatherData = await getWeatherData();
console.log("weatherData", weatherData);
</script>
