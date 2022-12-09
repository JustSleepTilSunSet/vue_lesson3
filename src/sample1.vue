  <template>
  <div class="sample1">
    <h1>sample1</h1>
    
    <draggable v-model="myArray" group="people" @start="drag = true" @end="draggable = false">
      <div v-for="element in myArray" :key="element.id" class = "optionSet" >
        <!-- @事件的意思，同v-on:事件，只是@會提示事件名稱而已-->
        <div v-bind:class="element.itemClass"  
         @dragover="dragOverHandler(element)"
         @dragleave="dragleaveHandler(element)"
         @drop="dragendHandler(element)"
         >
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
        itemClass:"optionContent"
      });
    }
  },
  methods:{
    dragOverHandler:(element)=>{
        console.log(JSON.stringify(element,null,2));
        element.itemClass = "optionEmpty";
    },
    dragenterHandler:(element, theEvent)=>{
      element.itemClass = "optionEmpty";
    },
    dragleaveHandler:(element)=>{
      console.log(JSON.stringify(element,null,2));
      element.itemClass = "optionContent";
    },
    dragendHandler:(element)=>{
      console.log(JSON.stringify(element,null,2));
      element.itemClass = "optionContent";
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
