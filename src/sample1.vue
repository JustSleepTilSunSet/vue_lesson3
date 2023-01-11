  <template>
  <div class="sample1">
    <h1>sample1</h1>
    
    <draggable v-model="myArray" group="people" @start="start" @end="end">
      <div v-for="element in myArray" :key="element.id" class = "optionSet" >
        <!-- @事件的意思，同v-on:事件，只是@會提示事件名稱而已-->
        <div v-bind:class="element.itemClass"
          @dragover="dragOverHandler(element)"
          @dragleave="dragleaveHandler(element)"
          @drop="dropHandler(element)"
          @drag="durationchangeHandler(element)"
         >
          {{ element.name }}
        </div>
      </div>
    </draggable>
    <div>
      {{this.RightItem}}
    </div>
  </div>
</template>
<script>
import draggable from 'vuedraggable'
import _ from 'lodash'

export default {
  props:{
    RightItem: Object
  },
  data() {
    return {
      myArray: [],
      index:0,
      replaceIdx:0
    };
  },
  beforeMount() {
    for (this.index = 0; this.index < 10; this.index++) {
      this.myArray.push({
        index: this.index,
        id: `s1_${this.index}`,
        name: `content${this.index}`,
        itemClass:"optionContent"
      });
    }
  },
  methods:{
    start(event){
      // console.log(event.oldDraggableIndex);
      // console.log(JSON.stringify(this.myArray[event.oldDraggableIndex],null,2));
      this.$emit("Left-Trigger", this.myArray[event.oldDraggableIndex]);
      // const findOverItem = (element) => this.myArray[event.oldDraggableIndex].id == element.id;
      // let idx = this.myArray.findIndex(findOverItem);
      // console.log(`idx: ${idx}`);
      // this.myArray.splice(idx, 1);
    },
    end(){
      this.myArray.pop();
    },
    dragOverHandler(element){
        element.itemClass = "optionEmpty";
    },
    dragleaveHandler(element){
        element.itemClass = "optionContent";
    },
    dropHandler(element){
      element.itemClass = "optionContent";
    }
  },
  components: {
     draggable
  },
  watch:{
    mainMsg:function(value){
      console.log(`收到 ${value}`);
    }
  }
};
</script>

<style>
@import "./css/testingCss.css";
</style>
