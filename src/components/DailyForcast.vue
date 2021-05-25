<template>
  <div class="parent-daily-forcast">
    <div class="ui-first-segment">
      <div class="ui-first-segment_city">
        {{ cityName }} <em class="emp"> ({{ countryName }})</em>
      </div>

      <div class="ui-first-segment_date">{{ currentDate }}</div>
    </div>
    <div class="ui-second-segment">
      <button class="ui-second-segment_state-succes" type="button">C</button>
      <button class="ui-second-segment_state-normal" type="button">F</button>
    </div>
  </div>
  <div class="ui-third-segment">
    <div class="ui-third-segment_icon">
      <img v-bind:src="this.url" alt="icon" />
    </div>
    <div class="ui-third-segment_temp">{{ temperature }}</div>
    <div class="ui-third-segment_desc">{{ description }}</div>
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
.ui-first-segment_city {
  font-size: 1.5rem;
}
.emp {
  font-size: 1rem;
}
.ui-second-segment {
  order: 5;
  align-self: center;
}

.ui-second-segment_state-succes {
  background-color: green;
  border-radius: 4px 0 0 4px;
  color: white;
}
.ui-second-segment_state-normal {
  background-color: gray;
  border-radius: 0 4px 4px 0;
  color: white;
}
.ui-third-segment {
  display: flex;
  justify-content: center;
  padding: 3rem;
  background-color: black;
  color: white;
}
.ui-third-segment_temp {
  font-size: 3rem;
}
.ui-third-segment_desc {
  align-self: flex-end;
}
</style>
