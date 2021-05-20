<template>
  <div class="parent">
    <div class="first-container">
      <div class="first-container_city">
        {{ cityName }} <em class="emp"> ({{ countryName }})</em>
      </div>
      <div class="first-container_date">20/5/2021</div>
    </div>
    <div class="second-container">
      <button class="second-container_left-button" type="button">btn1</button>
      <button class="second-container_right-button" type="button">btn2</button>
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
export default {
  name: "DailyForcast",
  props: ["temperature", "description", "cityName", "countryName", "iconCode"],
  data: function () {
    return {
      url: "https://www.weatherbit.io/static/img/icons/c04d.png",
    };
  },
  watch: {
    iconCode() {
      //if iconCode change, it will change in the url as well
      this.url = `https://www.weatherbit.io/static/img/icons/${this.iconCode}.png`;
    },
  },
};
</script>

<style>
.parent {
  display: flex;
  justify-content: space-around;
  padding: 2rem;
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
}
.parent-third-container_temp {
  font-size: 3rem;
}
.parent-third-container_desc {
  align-self: flex-end;
}
</style>
