<template>
  <div>{{ temperature }}</div>
  <div>{{ description }}</div>
  <div>{{ cityName }}</div>
  <div>{{ countryName }}</div>
</template>

<script>
export default {
  name: "DailyForcast",
  props: ["temperature", "description", "cityName", "countryName"],
  // data: function () {
  //   return {
  //     temperature: 25,
  //   };
  // },
};
</script>

<style>
</style>
