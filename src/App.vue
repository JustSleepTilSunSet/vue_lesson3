<template>
  <div id="app">
    <drop-manager></drop-manager>
  </div>
</template>

<script>
import dropManager from "./dropManager.vue";
export default {
  name: "App",
  components: {
    dropManager,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
