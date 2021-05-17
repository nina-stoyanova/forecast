<template>
  <main>
    <DropDown></DropDown>
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
  components: {
    DropDown,
    DailyForcast,
    WeeklyForcast,
  },
};
</script>

<style>
</style>
