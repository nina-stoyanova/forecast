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
