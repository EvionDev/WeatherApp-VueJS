<script setup>
import baseCard from "./components/baseCard.vue";
import { ref } from "vue";

const query = ref("");
const weatherData = ref(null);
const api_key = import.meta.env.VITE_API_KEY;

const url_base = "https://api.weatherapi.com/v1";

const date = new Date();
const options = { day: "numeric", month: "numeric", year: "numeric" };
const fullDate = new Intl.DateTimeFormat("pl-PL", options).format(date);

function fetchData(e) {
  if (e.key == "Enter") {
    fetch(`${url_base}/current.json?key=${api_key}&q=${query.value}`)
      .then((res) => {
        if (res.ok) {
          return res.json();
        }
      })
      .then(
        (json) =>
          (weatherData.value = {
            temp_c: json.current.temp_c,
            feelslike_c: json.current.feelslike_c,
            city: json.location.name,
            country: json.location.country,
            imgSrc: json.current.condition.icon,
            imgAlt: json.current.condition.text,
          })
      );
  }
}
</script>

<template>
  <base-card>
    <input
      type="text"
      class="bg-transparent py-2 px-3 outline-none border-2 border-black rounded-lg"
      placeholder="City..."
      v-model="query"
      @keypress="fetchData"
    />
    <div v-if="weatherData" class="flex items-center flex-col mt-4">
      <header class="flex items-center">
        <img
          :src="weatherData.imgSrc"
          :alt="weatherData.imgAlt"
          class="max-w-[50%] w-auto h-auto"
        />
        <div>
          <p>{{ weatherData.temp_c }}°C</p>
          <p v-if="weatherData.feelslike_c !== weatherData.temp_c">
            Feels {{ weatherData.feelslike_c }}°C
          </p>
        </div>
      </header>
      <main class="flex flex-col items-center">
        <h1 class="text-3xl underline">
          {{ weatherData.city }}
        </h1>
        <h3>
          {{ weatherData.country }}
        </h3>
        <p>{{ fullDate }}</p>
      </main>
    </div>
  </base-card>
</template>

<style>
body {
  background-color: #eaeaea;
  height: 100vh;
  width: 100vw;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
