<template>
  <div id="app">
    <drop-manager></drop-manager>
    <!-- <div>
      <h1>我是容器1</h1>
      <div style="margin-left:25% margin-right:25%">
        <div class="outerContainer">
          <DraggableSample1></DraggableSample1>
          <DraggableSample2></DraggableSample2>
        </div>
      </div>
    </div> -->
  </div>
</template>

<script>
// import DraggableSample1 from "./sample1.vue";
// import DraggableSample2 from "./sample2.vue";
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
