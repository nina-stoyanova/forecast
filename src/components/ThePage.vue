<template>
  <div>
    <main></main>
  </div>
  <DropDown></DropDown>
  <DailyForcast></DailyForcast>
  <WeeklyForcast></WeeklyForcast>
</template>

<script>
import DropDown from "./DropDown.vue";
import DailyForcast from "./DailyForcast.vue";
import WeeklyForcast from "./WeeklyForcast.vue";

export default {
  name: "ThePage",
  component: {
    DropDown,
    DailyForcast,
    WeeklyForcast,
  },
};
</script>

<style>
</style>
