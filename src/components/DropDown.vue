<template>
  <select @change="onChange" name="dropdown" id="city" class="dropdown">
    <option value="sofia">sofia</option>
  </select>
</template>

<script>
import * as countryList from "../data/city.js";

export default {
  name: "DropDown",
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
    console.log(cityArr);
  },

  methods: {
    onChange(eventInfo) {
      console.log(eventInfo);
    },
  },
  data: function () {
    return {
      cities: [],
    };
  },
};
</script>

<style>
</style>
