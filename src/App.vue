<template>
  <div id="app">
    <!-- 注意上一頁設計-->
    <!-- <PageA></PageA> -->
    <!-- <PageA @Submit-Trigger="SubmitTrigger"></PageA> -->
    <!-- <HelloWorld msg="Hello World!!"/> -->
    <!-- <div class="flex-container"> -->
    <DraggableLesson2></DraggableLesson2>
    <DraggableLesson></DraggableLesson>
    <!-- <DraggableLesson msg="清單列表2"/> -->
    <!-- <DraggableLesson msg="清單列表3"/> -->
    <!-- </div> -->
  </div>
</template>

<script>
// import PageA from './components/PageA.vue';
// import HelloWorld from './components/HelloWorld.vue';
import DraggableLesson2 from './components/DraggableLesson - 複製.vue';
import DraggableLesson from './components/DraggableLesson.vue';

export default {
  name: 'App',
  methods: {
    SubmitTrigger: function (val) {
      console.log(`embeded: ${val}`);
    }
  },
  beforeMount() {
    // this.$mount(PageA);
    // this.pageList.push(PageA);
  },
  data() {
    return {
      pageList: []
    }
  },
  components: {
    // HelloWorld,
    DraggableLesson2,
    DraggableLesson
    // PageA
  }
}
</script>

<style>
@import url('./css/RootCss.css');

html {
  max-width: 1440px;
  max-height: 1024px;
}
</style>
