<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Hello World!!"/>
    <div class="flex-container">
        <DraggableLesson msg="清單列表1"/>
        <DraggableLesson msg="清單列表2"/>
        <DraggableLesson msg="清單列表3"/>
    </div>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import DraggableLesson from './components/DraggableLesson.vue';

export default {
  name: 'App',
  components: {
    HelloWorld,
    DraggableLesson
  }
}
</script>

<style>
@import url('./css/RootCss.css') ;
</style>
