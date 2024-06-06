<template>
  <div class="weather">
    <h1>Weather App</h1>

    <input type="text" v-model="city" placeholder="Enter city" />

    <button @click="getWeather">Get Weather</button>

    <div v-if="weatherData">
      <p>Temperature: {{ weatherData.main.temp }}°C</p>

      <p>Weather: {{ weatherData.weather[0].main }}</p>

      <p>Description: {{ weatherData.weather[0].description }}</p>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "WeatherComponent",

  data() {
    return {
      city: "",

      weatherData: null,
    };
  },

  methods: {
    async getWeather() {
      try {
        const response = await axios.get(
          `https://api.openweathermap.org/data/2.5/weather?q=${this.city}&appid=3cf341164b71234f1c03f9d715db3c14&units=metric`
        );

        this.weatherData = response.data;
      } catch (error) {
        console.error(error);
      }
    },
  },
};
</script>

<style scoped>
.weather {
  text-align: center;

  margin-top: 50px;
}
</style>
