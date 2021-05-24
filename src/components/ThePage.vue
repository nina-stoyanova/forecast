<template>
  <main>
    <DropDown @selectedCityObject="onSelectedCity"></DropDown>
    <DailyForcast
      v-bind:cityName="cityName"
      v-bind:countryName="countryName"
      v-bind:temperature="temp"
      v-bind:description="desc"
      v-bind:iconCode="iCode"
    ></DailyForcast>
    <WeeklyForcast
      v-bind:arrayWeeklyRequest="arrayWeeklyRequest"
    ></WeeklyForcast>
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
      selectedCityObject: "", //we save the selected city as data propert
      arrayDailyRequest: [],
      temp: 0,
      desc: "",
      cityName: "",
      countryName: "",
      iCode: "",
      arrayWeeklyRequest: [],
      objWeeklyRequest: {},
    };
  },
  components: {
    DropDown,
    DailyForcast,
    WeeklyForcast,
  },
  methods: {
    getWeatherResponse() {
      fetch(
        `https://api.weatherbit.io/v2.0/current?key=fafa69308bd244c49215c6f89c37b286&city=${selectedCityObject.cityName}&country=${selectedCityObject.countryCode}`
      )
        .then((response) => {
          return response.json();
        })
        .then((data) => {
          this.arrayDailyRequest = data.data;
          let arr = this.findCity();
          this.setProperties(arr);
        })
        .catch(() => {});
    },
    /**
     * Set up properties from the request data
     */
    setProperties(arr) {
      this.temp = arr.temp;
      this.desc = arr.weather.description;
      this.cityName = arr.city_name;
      this.countryName = selectedCityObject.countryName;
      this.iCode = arr.weather.icon;
    },
    /**
     * Find the city with the selected name
     */
    findCity() {
      let arr = this.arrayDailyRequest.find((element) => {
        return element.city_name === selectedCityObject.cityName;
      });
      return arr;
    },

    onSelectedCity(selectedCityObject) {
      this.selectedCityObject = selectedCityObject;
      this.loadWeatherData();
      fetch(
        `https://api.weatherbit.io/v2.0/forecast/daily?key=fafa69308bd244c49215c6f89c37b286&city=${selectedCityObject.cityName}&country=${selectedCityObject.countryCode}&days=5`
      )
        .then((response) => {
          return response.json();
        })
        .then((result) => {
          if (result.city_name === selectedCityObject.cityName) {
            let arr = result.data;
            this.arrayWeeklyRequest = [];
            for (let i = 0; i < arr.length; i++) {
              let element = arr[i];
              let date = arr[i].datetime;
              let stringDate = moment(date).format("dddd"); // here we change 20.20.2021 to Friday for example
              let maxTemp = element.max_temp;
              let minTemp = element.min_temp;
              let icon = element.weather.icon;
              this.objWeeklyRequest = {
                maxTemp,
                minTemp,
                icon,
                stringDate,
              };
              this.arrayWeeklyRequest.push(this.objWeeklyRequest);
            }
          }
        });
    },
  },
};
</script>

<style>
</style>
