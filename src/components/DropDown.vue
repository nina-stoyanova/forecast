<template>
  <select @change="onChange" name="dropdown" id="count" class="dropdown">
    <option
      v-for="city in cityArray"
      :key="city.cityName"
      v-bind:value="city.cityName"
    >
      {{ city.cityName }} {{ city.countryName }}
    </option>
  </select>
</template>

<script>
import { countryList } from "../data/country.js";

export default {
  name: "DropDown",
  emits: ["selectedCityObject"],
  data: function () {
    return {
      cityArray: [], //we have the array with objects(not sure if we need this)
    };
  },
  mounted() {
    let cityArr = [];
    for (let i = 0; i < countryList.length; i++) {
      let country = countryList[i];
      for (let j = 0; j < country.cities.length; j++) {
        let city = country.cities[j]; //the object that holds cityname, country name and code is city
        cityArr.push({
          cityName: city.name,
          countryName: country.name,
          countryCode: country.iso2,
        });
      }
    }
    this.cityArray = cityArr;
  },

  methods: {
    onChange(event) {
      let selectedCity = event.target.value; //selectedCity = name of the selected city
      let selectedCityObject = this.cityArray.find((element) => {
        //the object of the selected city
        return element.cityName === selectedCity; // returns the object of the selected city
      });

      this.$emit("selectedCityObject", selectedCityObject); //we send the object of the selected city
    },
  },
};
</script>

<style>
.dropdown {
  width: 100%;
}
</style>
