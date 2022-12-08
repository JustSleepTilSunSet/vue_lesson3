<template>
  <div class="sample1">
    <h1>sample1</h1>
    
    <draggable v-model="myArray" group="people" :move="checkMove" @start="drag = true" @end="handleDraggEnd($event)">
      <div v-for="element in myArray" :key="element.id" class="optionSet" :draggable="handleDraggEnd(element)">
        <div class="optionContent">
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
    };
  },
  beforeMount() {
    let index;
    for (index = 0; index < 10; index++) {
      this.myArray.push({
        id: `s${index}`,
        name: `content${index}`,
      });
    }
  },
  methods:{
    handleDraggEnd:($e)=>{
        console.log($e)
    },
    handleDragg:(element)=>{
        console.log(element);
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
