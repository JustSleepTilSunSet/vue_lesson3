<template>
  <div class="sample2">
    <h1>sample2</h1>
    <draggable v-model="myArray" group="people" @start="drag = true" @end="drag = false">
      <div v-for="element in myArray" :key="element.id" class="optionSet">
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
        id: `s2_${index}`,
        name: `content${index}`,
      });
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
