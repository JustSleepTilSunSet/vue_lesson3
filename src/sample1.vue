  <template>
  <div class="sample1">
    <h1>To-Do List</h1>
    
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
      sample2送到sample1:
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
      replaceIdx:0,
      isMoveBySelf: true
    };
  },
  beforeMount() {
    for (this.index = 0; this.index < 10; this.index++) {
      this.myArray.push({
        index: this.index,
        id: `s1_${this.index}`,
        name: `content${this.index}`,
        itemClass:"optionContent",
        isReBack:false,
        isAblePop: false
      });
    }
  },
  methods:{
    start(event){
      this.$emit("Left-Trigger", this.myArray[event.oldDraggableIndex]);
    },
    end(){
      if(this.myArray[this.myArray.length-1].isAblePop)
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
      if( element.isReBack && element.id.includes('s1_')){
        let rebackItemIdx = this.myArray.findIndex((e)=> e.id==element.id);
        this.myArray.splice(rebackItemIdx,rebackItemIdx);
        alert("禁止回流物件!強制執行drop!");
      }
    }
  },
  components: {
     draggable
  },
  watch:{
    mainMsg:function(value){
      console.log(`mainMsg ${value}`); 
    }
  }
};
</script>

<style>
@import "./css/testingCss.css";
</style>
