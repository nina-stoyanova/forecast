<template>
  <div class="parent-weekly-forcast">
    <ul class="ul">
      <li>{{format(day)}}</li>
      <li><img v-bind:src="getIconUrl" alt="icon" />
      </li>
      <li>Min {{ minT}} Max {{ maxT }}</li>
    </ul>
  </div>

</template>-

<script>
import moment from "moment";
export default {
  name: "WeeklyForcast",
  props: ["day","icon","minT","maxT"],
  computed:{
     getIconUrl() {
     return`https://www.weatherbit.io/static/img/icons/${this.icon}.png`;
    },
  },
  methods: {
       format(stringDate){
      return  moment(stringDate).format("dddd");
    }
  }
  
};
/* 
              let stringDate = moment(arr[i].datetime).format("dddd"); // here we change 20.20.2021 to Friday for example
              let maxTemp = element.max_temp;
              let minTemp = element.min_temp;
              let icon = element.weather.icon;
              this.objWeeklyRequest = {
                maxTemp,
                minTemp,
                icon,
                stringDate,
              };
              this.arrayWeeklyRequest.push(this.objWeeklyRequest);
            }
            */
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
