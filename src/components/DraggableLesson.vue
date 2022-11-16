<template>
    <div class="item">
        <h3>{{ msg }}</h3>
        <draggable v-model="myArray" group="people" @start="drag = true" @end="drag = false">
            <div class = "item_setting" v-for="element in myArray" :key="element.id">{{ element.name }}</div>
        </draggable>
    </div>
</template>
<script>
import Draggable from 'vuedraggable';
export default {
    props: {
        msg: String
    },
    data() {
        return {
            myArray:[]
        }
    },
    beforeMount() {
        for(let index=1; index<=5;index++){
            this.myArray.push({
                id: index,
                name: `項目${index}`
            })
        }
        console.log(JSON.stringify(this.myArray,null,2));
    },
    components: {
        Draggable
    }
}

</script>
<style>
@import url('../css/DraggableLesson.css');
</style>