<template>
  <TheHeader></TheHeader>
  <ThePage></ThePage>
</template>

<script>
import TheHeader from "./components/TheHeader.vue";
import ThePage from "./components/ThePage.vue";

export default {
  name: "App",
  components: {
    TheHeader,
    ThePage,
  },
};
</script>

<style>
* {
  border: 1px solid red;
}
</style>
