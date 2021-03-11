<template>
  <section class="weather-app">
    <div class="container">
      <div class="row justify-content-center">
        <div class="col-md-8">
          <h1>weather app</h1>
          <select v-model="city" @change="getData()" class="form-control">
            <option v-for="city in allCities" :key="city.index">{{city.capital}}</option>
          </select>
          <div v-if="city" class="row">
            <div class="col-md-12">
              <p>{{ city }}</p>
            </div>
            <div class="col-md-6 text-center">
              <p>Temprature is {{ apiData.list[0].main.temp }} <sup>o</sup></p>
            </div>
            <div class="col-md-6 text-center">
              <p>Status is {{ apiData.list[0].weather[0].main }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
<script>
import axios from "axios";
export default {
  name: "App",
  data() {
    return {
      city: "",
      apiData: [],
      allCities: [],
    };
  },
  methods: {
    getData() {
      axios
        .get(
          `http://api.openweathermap.org/data/2.5/find?q=${this.city}&units=metric&appid=bc4f20d5a7c23a6e726c2f90b4014fea`
        )
        .then((e) => {
          this.apiData = e.data;
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
  created() {
    axios
      .get("https://restcountries.eu/rest/v2/all")
      .then((e) => {
        this.allCities = e.data;
      })
      .catch((error) => {
        console.log(error);
      });
  },
};
</script>
<style>
.weather-app {
  background: url(../src/assets/images/night.webp);
  background-size: cover;
  width: 70%;
  height: 80%;
  margin: auto;
}
.weather-app h1 {
  color: white;
  font-weight: bold;
  margin: 30px auto;
  text-align: center;
} 
.weather-app p {
  color: white;
  font-weight: bold;
  font-size: 30px;
  text-align: center;
  margin: 30px auto;
  border-radius: 20px;
  background: rgba(0, 0, 0, .3);
}
</style>
