<template>
    <!--導傳元件-->
    <div>
      <h1>我是容器1</h1>
      <div style="margin-left:25% margin-right:25%">
        <div class="outerContainer">
          <DraggableSample1 @Left-Trigger="LeftHandler" :RightItem="RightItem"></DraggableSample1>
          <DraggableSample2 @Right-Trigger="RightHandler" :LeftItem="LeftItem"></DraggableSample2>
        </div>
      </div>
    <button @click="clickHandler"> hhhhhhhh </button>
    </div>
</template>


<script>
import DraggableSample1 from './sample1.vue';
import DraggableSample2 from './sample2.vue';

export default {
  components: {
    DraggableSample1,
    DraggableSample2
  },
   data() {
    return {
        RightItem:{},
        LeftItem:{}
    };
  },
  methods:{
    LeftHandler(value){
        this.LeftItem = value;
    },
    RightHandler(value){
      this.RightItem = value;
    },
    clickHandler(){
        this.helloMsg += "h";
    }
  }
}
</script>


<style>

</style>