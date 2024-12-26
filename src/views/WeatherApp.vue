<template>
      <div class="lg:absolute lg:ml-96">
      <img src="/240_F_579861052_KjeAAbyaXOBY6JjxMEPBVJypp2KSb59v.jpg" alt="" class="lg:ml-40 lg:w-11/12">
    </div>
    <div class=" lg:relative  lg:mr-96 lg:ml-96 ml-2 mr-2 mt-20 pb-2 bg-zinc-300 rounded-md font-serif lg:font-serif lg:py-20">

      <div class="lg:-mt-24 lg:p-4">
        <h1 class="font-bold mb-4 pt-2 text-white lg:text-xl lg:pt-4">Weather App</h1>
      <input
        type="text"
        placeholder="search..."
        v-model="query"
        class="lg:w-64 lg:rounded-md lg:ml-10 w-64 h-10 rounded-lg outline-none"
      />
      <button
        @click="fetchWeather"
        class="lg:bg-cyan-900 bg-cyan-900 ml-4 px-4 py-1 lg:px-8 lg:py-2 mb-4 rounded-md lg:rounded-md text-white lg:border-2 lg:border-white"
      >
        Submit
      </button>
      <div v-if="weather && weather.main" class="lg:w-64 lg:h-64 lg:shadow-md lg:text-center lg:ml-64 w-64 h-64 shadow-md rounded-full text-center ml-10 pt-20 -mt-8 mb-2 text-white lg:text-white">
        <div class="lg:-mt-10">
          <p>{{ weather.name }}, {{ weather.sys.country }}</p>
        </div>
        <div>
          <p>Tempreture: {{ weather.main.temp }}°c</p>
        </div>
        <div>
            <p>Humidity: {{ weather.main.humidity }}%</p>
        </div>
        <div>
            <p>wind speed: {{ weather.wind.speed }}m/s</p>
        </div>
        <div>
            <p>Description: {{ weather.weather[0].description }}</p>
        </div>
        <div>
            <p>status: {{ weather.weather[0].main }}</p>
        </div>
      </div>

      </div>
           
      
    </div>

   
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    data() {
      return {
        api_key: '6fb14252943e50182260d6ef8d533590',
        query: '',
        weather: {},
      };
    },
    methods: {
      fetchWeather() {
        if (!this.query) {
          alert('Please enter a city name.');
          return;
        }
        const URL = `https://api.openweathermap.org/data/2.5/weather?q=${this.query}&appid=${this.api_key}&units=metric`;
        axios.get(URL)
          .then(res => {
            this.weather = res.data;
            this.query = ''
          })
          .catch(error => {
            console.error('Error fetching weather data:', error);
            alert('Could not fetch weather data. Please check the city name.');
          });
      },
    },
  };
  </script>
  
  <style scoped>

  body{
    background-color: rgb(210, 210, 210);
  }
  </style>