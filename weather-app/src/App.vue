<script setup>
import baseCard from "./components/baseCard.vue";
import imageProp from "./components/imageTag.vue";
import { ref } from "vue";

const query = ref("");
const weather = ref(null);
const api_key = import.meta.env.VITE_API_KEY;

const url_base = "https://api.weatherapi.com/v1";

const d = new Date();
const fullDate = `${d.getDate()} - ${
  d.getMonth() + 1 < 10 ? "0" + (d.getMonth() + 1) : d.getMonth() + 1
} -  ${d.getFullYear()}`;

function fetchData(e) {
  if (e.key == "Enter") {
    fetch(`${url_base}/current.json?key=${api_key}&q=${query.value}`)
      .then((res) => {
        if (res.ok) {
          return res.json();
        }
      })
      .then((json) => (weather.value = json));
  }
}

function img(value) {
  return weather.value.current.condition[value];
}

function temp(value) {
  return weather.value.current[value];
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
    <div v-if="weather" class="flex items-center flex-col mt-4">
      <header class="flex items-center">
        <image-prop
          :src="img('icon')"
          :alt="img('text')"
          class="max-w-[50%] w-auto h-auto"
        ></image-prop>
        <div>
          <p>{{ temp("temp_c") }}°C</p>
          <p v-if="temp('feelslike_c') !== temp('temp_c')">
            Feels {{ temp("feelslike_c") }}°C
          </p>
        </div>
      </header>
      <main class="flex flex-col items-center">
        <h1 class="text-3xl underline">
          {{ weather.location.name }}
        </h1>
        <h3>
          {{ weather.location.country }}
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
