<template>
  <div class="parent-daily-forcast">
    <div class="first-container">
      <div class="first-container_city">
        {{ cityName }} <em class="emp"> ({{ countryName }})</em>
      </div>
      <div class="first-container_date">{{ currentDate }}</div>
    </div>
    <div class="second-container">
      <button class="second-container_left-button" type="button">C</button>
      <button class="second-container_right-button" type="button">F</button>
    </div>
  </div>
  <div class="parent-third-container">
    <div class="parent-third-container-main-icon">
      <img v-bind:src="this.url" alt="icon" />
    </div>
    <div class="parent-third-container_temp">{{ temperature }}</div>
    <div class="parent-third-container_desc">{{ description }}</div>
  </div>
</template>

<script>
import moment from "moment";

export default {
  name: "DailyForcast",
  props: ["temperature", "description", "cityName", "countryName", "iconCode"],
  data: function () {
    return {
      url: "https://www.weatherbit.io/static/img/icons/c04d.png",
      currentDate: "",
    };
  },
  created() {
    this.getNow();
    this.currentDate = this.getCurrentDateTime();
  },
  watch: {
    iconCode() {
      //if iconCode change, it will change in the url as well
      this.url = `https://www.weatherbit.io/static/img/icons/${this.iconCode}.png`;
    },
  },
  methods: {
    getCurrentDateTime() {
      return moment().format("dddd MMMM-DD HH:mm"); //function returns object
    },
    getNow: function () {
      const today = new Date();
      const date =
        today.getFullYear() +
        "-" +
        (today.getMonth() + 1) +
        "-" +
        today.getDate();
      const time =
        today.getHours() + ":" + today.getMinutes() + ":" + today.getSeconds();
      const dateTime = date + " " + time;
      this.currentDate = dateTime;
    },
  },
};
</script>

<style>
.parent-daily-forcast {
  display: flex;
  justify-content: space-around;
  padding: 2rem;
  background-color: black;
  color: white;
}
.first-container_city {
  font-size: 1.5rem;
}
.emp {
  font-size: 1rem;
}
.second-container {
  order: 5;
  align-self: center;
}

.second-container_left-button {
  background-color: green;
  border-radius: 4px 0 0 4px;
  color: white;
}
.second-container_right-button {
  background-color: gray;
  border-radius: 0 4px 4px 0;
  color: white;
}
.parent-third-container {
  display: flex;
  justify-content: center;
  padding: 3rem;
  background-color: black;
  color: white;
}
.parent-third-container_temp {
  font-size: 3rem;
}
.parent-third-container_desc {
  align-self: flex-end;
}
</style>
