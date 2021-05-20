<template>
  <header class="header">
    <div class="container">What's the weather like in..?</div>
  </header>
  <div class="empty-line"></div>
</template>

<script>
export default {
  name: "TheHeader",
};
</script>

<style>
.header {
  background-color: black;
}
.container {
  font-weight: bold;
  color: white;
  padding: 20px;
}
.empty-line {
  background-color: gray;
  padding: 1px;
}
</style>
