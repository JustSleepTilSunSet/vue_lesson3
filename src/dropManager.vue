<template>
    <!--導傳元件-->
    <div>
      <h1>to-do list</h1>
      <div style="margin-left:25% margin-right:25%">
        <div class="outerContainer">
          <DraggableSample1 @Left-Trigger="LeftHandler" :RightItem="RightItem"></DraggableSample1>
          <DraggableSample2 @Right-Trigger="RightHandler" :LeftItem="LeftItem"></DraggableSample2>
        </div>
      </div>
    <button @click="clickHandler" class="button button2"> {{this.helloMsg}} </button>
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
        helloMsg:"Restart",
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
        this.RightItem={};
        this.helloMsg="Restart";
        this.LeftItem={};
        location.reload();
    }
  }
}
</script>


<style>

.button {
  background-color: #4CAF50; /* Green */
  border: none;
  color: white;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 20px;
  margin: 4px 2px;
  cursor: pointer;
}
.button2 {width: 50%;}
</style>