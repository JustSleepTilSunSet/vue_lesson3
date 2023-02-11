<template>
  <div class="sample2">
    <h1>Priority queue</h1>
    <draggable :options="{disabled : true}" v-model="myArray" group="people" @start="draggable = true" @end="draggable = true">
      <div v-for="element in myArray" :key="element.id" class="optionSet" >
        <div v-bind:class="element.itemClass"
        @dragover="dragoverHandler(element,$event)"
        @drop="dropHandler(element)"
        @dragenter="dragenterHandler(element)"
        v-on:>
          {{ element.name }}
        </div>
      </div>
    </draggable>
    <div>
      收到sample2
      {{this.LeftItem}}
    </div>
  </div>
</template>
<script>
import draggable from 'vuedraggable'
export default {
  props:{
    LeftItem: Object,
    isRightMoveDone:false
  },
  data() {
    return {
      myArray: [],
      savedArray:[],
      overItem: null,
      optionContent:["優先度最高", "優先度高", "優先度中等", "優先度低"],
      resumeItems:[],
      resumeItemIdx:[],
      resumeSet: null
    };
  },
  methods:{
    dragoverHandler(element, event){
      //id為s1類的不會再被取代了。
      if(!(element.id).includes("s1_")){
        element.itemClass = "insteadContent";
        this.overItem = element;
      }

      //若沿路上發生取代，則恢復id為s2的元件。
      if((element.id).includes("s2_") && this.resumeItems.findIndex((ele)=> ele.id == element.id) < 0){
        this.resumeItems.push(element);
        this.resumeItemIdx.push(element.index);
      }
      if(this.resumeItems.length > 1 && element.id.includes("s2_")){
        let preItem = this.resumeItems.shift();
        let preItemIdx = this.resumeItemIdx.shift();
        this.myArray.findIndex((ele)=> ele.id == preItem.id);
        preItem.itemClass = "optionContent";
        this.myArray[preItemIdx] = preItem;
      }

      this.$emit("Right-Trigger", this.overItem);
    },

    dropHandler(element){
      console.log(`Dropping.`);
      console.log(`dropHandler s2 element: ${JSON.stringify(element,null,2)}`);
      if(element.id.includes("s1_")){
        element.itemClass = "optionContent";
      }
    },
    dragenterHandler(element){
      console.log(`sample2 dragenterHandler:${JSON.stringify(element,null,2)}`);
      element.isReBack = true;
      element.isAblePop = true;
    }
  },
  beforeMount() {
    let index;
    for (index = 0; index < 4; index++) {
      this.myArray.push({
        index:index,
        id: `s2_${index}`,
        name: this.optionContent[index],
        itemClass:"optionContent"
      });
    }
  },
  components: {
     draggable
  },
  watch:{
    overItem:function(value){//恢復上一個
      console.log(`收到sample2 ${JSON.stringify(value,null,2)}`);
      const findOverItem = (element) => this.overItem.id == element.id;
      let idx = this.myArray.findIndex(findOverItem);
      this.myArray[idx] = this.LeftItem;
    },
    LeftItem:function(val){
      this.resumeItems = [];
      this.resumeItemIdx = [];
    }
  }
};
</script>

<style>
@import "./css/testingCss.css";
</style>
