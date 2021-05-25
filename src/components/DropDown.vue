<template>
  <div class="container">
    <select @change="onChange" name="dropdown" id="count" class="dropdown">
      <option
        v-for="city in cityArray"
        :key="city.cityName"
        v-bind:value="city.cityName"
      >
        {{ city.cityName }}
      </option>
    </select>
  </div>
</template>

<script>
import { countryList } from "../data/country.js";

export default {
  name: "DropDown",
  emits: ["selectedCities"],
  data: function () {
    return {
      cityArray: [],
    };
  },
  /**
   * Get city object from country list and fill in array with set up properties
   */
  mounted() {
    let cityArr = [];
    for (let i = 0; i < countryList.length; i++) {
      let country = countryList[i];
      for (let j = 0; j < country.cities.length; j++) {
        let city = country.cities[j];
        cityArr.push({
          cityName: city.name,
          countryName: country.name,
          countryCode: country.iso2,
        });
      }
    }
    this.cityArray = cityArr;
  },
  /**
   * Get selected value, compare it with cityName from the array and emit event name and event object
   */
  methods: {
    onChange(event) {
      let selectedCity = event.target.value;
      let selectedCities = this.cityArray.find((element) => {
        return element.cityName === selectedCity;
      });

      this.$emit("selectedCities", selectedCities);
    },
  },
};
</script>

<style>
.container {
  display: flex;
  justify-content: center;
  background-color: black;
}
.dropdown {
  width: 98%;
  padding: 10px;
  border-radius: 5px;
}
</style>
