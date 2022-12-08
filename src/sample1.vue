<template>
  <div class="sample1">
    <h1>sample1</h1>
    
    <draggable v-model="myArray" group="people" @start="drag = true" @end="handleDragEnd($event)">
      <div v-for="element in myArray" :key="element.id" class = "optionSet" :draggable="handleDragEnd(element)">
        <div v-bind:class="element.itemclass" v-on:dragleave ="handleClick(element, myArray)">
          {{ element.name }}
        </div>
          
      </div>
    </draggable>
  </div>
</template>
<script>
import draggable from 'vuedraggable'
export default {
  data() {
    return {
      myArray: [],
      index:0
    };
  },
  beforeMount() {
    for (this.index = 0; this.index < 10; this.index++) {
      this.myArray.push({
        index: this.index,
        id: `s1_${this.index}`,
        name: `content${this.index}`,
        itemclass:"optionContent"
      });
    }
  },
  methods:{
    handleDragEnd:($e,index)=>{
        // console.log($e)
    },
    handleDragg:(element)=>{
        // console.log(element);
    },
    handleClick:(ele, myArray)=>{
      console.log(`is draggle ${ele.index}`);
      console.log(`${JSON.stringify(myArray,null,2)}`);
      myArray.push({
        index: this.index,
        id: `s1_${this.index}`,
        name: `content${this.index}`,
        itemclass:"optionEmpty"
      });
      // this.myArray[ele.index].itemclass = "optionEmpty";
      // ele.itemclass = ele.isClick? "optionContent": "optionEmpty";
      // ele.isClick = !ele.isClick;
    }
  },
  components: {
     draggable
  },
};
</script>

<style>
@import "./css/testingCss.css";
</style>
