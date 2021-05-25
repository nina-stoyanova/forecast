<template>
  <div v-if="weeklyRequests.length > 1" class="parent-weekly-forcast">
    <ul v-for="element in weeklyRequests" :key="element" class="ul">
      <li>{{ element.stringDate }}</li>
      <li>
        <img v-bind:src="getIconUrl(element.icon)" alt="icon" />
      </li>
      <li>Max {{ element.maxTemp }} Min {{ element.minTemp }}</li>
    </ul>
  </div>
  <div class="footer">black space</div>
</template>

<script>
export default {
  name: "WeeklyForcast",
  props: ["weeklyRequests"],
  methods: {
    /**
     * get the code for the needed icon
     */
    getIconUrl(iconCode) {
      return `https://www.weatherbit.io/static/img/icons/${iconCode}.png`;
    },
  },
};
</script>

<style>
.parent-weekly-forcast {
  display: flex;
  justify-content: space-evenly;
  background-color: black;
  color: white;
}
.ul {
  list-style-type: none;
  margin: 0;
  padding: 0;
}
.footer {
  background-color: black;
  padding: rem;
}
</style>
