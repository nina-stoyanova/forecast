<template>
  <main>
    <DropDown @selectedCity="onSelectedCity"></DropDown>
    <DailyForcast></DailyForcast>
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
      citySelected: "", //we save the selected city as data property
    };
  },
  components: {
    DropDown,
    DailyForcast,
    WeeklyForcast,
  },
  methods: {
    onSelectedCity(selectedCity) {
      this.citySelected = selectedCity;
      console.log(this.citySelected);
    },
  },
};
</script>

<style>
</style>
