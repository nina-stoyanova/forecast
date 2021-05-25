<template>
  <main>
    <DropDown @selectedCities="onSelectedCity"></DropDown>
    <DailyForcast
      v-bind:cityName="cityName"
      v-bind:countryName="countryName"
      v-bind:temperature="temp"
      v-bind:description="desc"
      v-bind:iconCode="iCode"
    ></DailyForcast>
    <WeeklyForcast v-bind:weeklyRequests="weeklyRequests"></WeeklyForcast>
  </main>
</template>

<script>
import DropDown from "./DropDown.vue";
import DailyForcast from "./DailyForcast.vue";
import WeeklyForcast from "./WeeklyForcast.vue";
import moment from "moment";

export default {
  name: "ThePage",
  data: function () {
    return {
      selectedCities: {},
      dailyRequests: [],
      temp: 0,
      desc: "",
      cityName: "",
      countryName: "",
      iCode: "",
      weeklyRequests: [],
      weeklyProperties: {},
    };
  },
  components: {
    DropDown,
    DailyForcast,
    WeeklyForcast,
  },
  methods: {
    /**
     * Reright the selected city
     */
    onSelectedCity(selectedCities) {
      this.selectedCities = selectedCities;
      this.getCurrentWeatherResponse();
      this.getDailyWeatherResponse();
    },
    /**
     * Get current weather response
     */
    getCurrentWeatherResponse() {
      fetch(
        `https://api.weatherbit.io/v2.0/current?key=fafa69308bd244c49215c6f89c37b286&city=${this.selectedCities.cityName}&country=${this.selectedCities.countryCode}`
      )
        .then((response) => {
          return response.json();
        })
        .then((data) => {
          this.dailyRequests = data.data;
          let arr = this.findCity();
          this.setProperties(arr);
        })
        .catch(() => {});
    },
    /**
     * Find the city with the selected name and compare it with the response city
     */
    findCity() {
      let arr = this.dailyRequests.find((element) => {
        return element.city_name === this.selectedCities.cityName;
      });
      return arr;
    },
    /**
     * Set up properties from the request data
     */
    setProperties(arr) {
      this.temp = arr.temp;
      this.desc = arr.weather.description;
      this.cityName = arr.city_name;
      this.countryName = this.selectedCities.countryName;
      this.iCode = arr.weather.icon;
    },
    /**
     * Get daily weather response, fill in dailyForcasts with set up properties
     */
    getDailyWeatherResponse() {
      fetch(
        `https://api.weatherbit.io/v2.0/forecast/daily?key=fafa69308bd244c49215c6f89c37b286&city=${this.selectedCities.cityName}&country=${this.selectedCities.countryCode}&days=5`
      )
        .then((response) => {
          return response.json();
        })
        .then((result) => {
          if (result.city_name === this.selectedCities.cityName) {
            let arr = result.data;
            this.weeklyRequests = [];
            for (let i = 0; i < arr.length; i++) {
              let element = arr[i];
              let date = arr[i].datetime;
              let stringDate = moment(date).format("dddd");
              let maxTemp = element.max_temp;
              let minTemp = element.min_temp;
              let icon = element.weather.icon;
              this.weeklyProperties = {
                maxTemp,
                minTemp,
                icon,
                stringDate,
              };
              this.weeklyRequests.push(this.weeklyProperties);
            }
          }
        });
    },
  },
};
</script>

<style>
</style>
