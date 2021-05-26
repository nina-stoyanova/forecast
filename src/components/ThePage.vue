<template>
  <main>
    <DropDown @selectedCityObject="onSelectedCity"></DropDown>
    <DailyForcast
      v-bind:cityName="cityName"
      v-bind:countryName="countryName"
      v-bind:temperature="temperature"
      v-bind:description="description"
      v-bind:iconCode="iconCode"
    ></DailyForcast>
    <div v-if="arrayWeeklyRequest.length > 1" class="parent-weekly-forcast">
      <WeeklyForcast
        v-for="element in arrayWeeklyRequest"
        :key="element"
        v-bind:day="element.datetime"
        v-bind:icon="element.weather.icon"
        v-bind:minT="element.min_temp"
        v-bind:maxT="element.max_temp"
      ></WeeklyForcast>
    </div>
  </main>
</template>

<script>
import DropDown from "./DropDown.vue";
import DailyForcast from "./DailyForcast.vue";
import WeeklyForcast from "./WeeklyForcast.vue";

export default {
  name: "ThePage",
  data: function () {
    return {
      selectedCityObject: "", //we save the selected city as data propert
      arrayDailyRequest: [],
      temperature: 0,
      description: "",
      cityName: "",
      countryName: "",
      iconCode: "",
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
    onSelectedCity(selectedCityObject) {
      this.selectedCityObject = selectedCityObject;
      this.getWeatherResponse();
      this.getDailyWeather();
    },
    getWeatherResponse() {
      fetch(
        `https://api.weatherbit.io/v2.0/current?key=fafa69308bd244c49215c6f89c37b286&city=${this.selectedCityObject.cityName}&country=${this.selectedCityObject.countryCode}`
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
     * Find the city with the selected name
     */
    findCity() {
      let arr = this.arrayDailyRequest.find((element) => {
        return element.city_name === this.selectedCityObject.cityName;
      });
      return arr;
    },
    /**
     * Set up properties from the request data
     */
    setProperties(arr) {
      this.temperature = arr.temp;
      this.description = arr.weather.description;
      this.cityName = arr.city_name;
      this.countryName = this.selectedCityObject.countryName;
      this.iconCode = arr.weather.icon;
    },

    getDailyWeather() {
      fetch(
        `https://api.weatherbit.io/v2.0/forecast/daily?key=fafa69308bd244c49215c6f89c37b286&city=${this.selectedCityObject.cityName}&country=${this.selectedCityObject.countryCode}&days=5`
      )
        .then((response) => {
          return response.json();
        })
        .then((result) => {
          if (result.city_name === this.selectedCityObject.cityName) {
            let arr = result.data;
            this.arrayWeeklyRequest = [];
            for (let i = 0; i < arr.length; i++) {
              let element = arr[i];
              this.arrayWeeklyRequest.push(element);
            }
          }
        });
    },
  },
};
</script>

<style>
</style>

