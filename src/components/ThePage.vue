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
    <WeeklyForcast></WeeklyForcast>
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
      arrayRequest: [],
      temp: 0,
      desc: "",
      cityName: "",
      countryName: "",
      iCode: "",
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
      //console.log(selectedCityObject.cityName);

      fetch(
        `https://api.weatherbit.io/v2.0/current?key=fafa69308bd244c49215c6f89c37b286&city=${selectedCityObject.cityName}&country=${selectedCityObject.countryCode}`
      )
        .then((response) => {
          return response.json();
        })
        .then((data) => {
          this.arrayRequest = data.data;
          //console.log(this.arrayRequest);
          let arr = this.arrayRequest.find((element) => {
            return element.city_name === selectedCityObject.cityName;
          });
          this.temp = arr.temp;
          this.desc = arr.weather.description;
          this.cityName = arr.city_name;
          this.countryName = selectedCityObject.countryName;
          this.iCode = arr.weather.icon;
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
};
</script>

<style>
</style>
