<template>
    <div v-if="synValue">
        <!-- <draggable class="item" v-model="myArray" @change="handleDragEvent_SecondHalf($event)" group="people" @start="drag = true"
            @end="drag = false">
            <div class="item_setting" v-for="element in myArray.slice(0, 5)" :key="element.id">{{ element.name }}
            </div>
        </draggable> -->

        <draggable class="bg_left" v-model='myArray' @change="handleDragEvent_OneHalf($event)" group="people"
            @start="drag = true" @end="handleEnd($event)">
            <div v-bind:class="element.class" v-for="element in myArray.slice(0, 4)" :key="element.id">{{ element.name }}
            </div>
        </draggable>

        <draggable class="backlog" v-model="myArray" @change="handleDragEvent_SecondHalf($event)" group="people"
            @start="drag = true" @end="drag = false">
            <div v-bind:class="element.class" v-for="element in myArray.slice(4, 10)" :key="element.id">
                {{ element.name }}
            </div>
        </draggable>
        <!-- <button v-on:click="testing">hh</button> -->
    </div>
</template>
<script>
import Draggable from 'vuedraggable';
export default {
    props: ["goC"],
    data() {
        return {
            myArray: [],
            cpy_myArray: [],
            oldIndex: 0,
            newIndex: 0,
            isMoved_OneHalf:false
        }
    },
    methods: {
        finish: function (item) {
            console.log(item.moved.element) // { id: 1, name: 'Item 1' }
        },
        handleDragEvent_OneHalf(e) {
            console.log(`${Object.keys(e)}`);
            this.isMoved_OneHalf = Object.keys(e)=="moved"; 
            console.log(`isMove ${this.isMoved_OneHalf}`);
            if (Object.keys(e) == "removed") {
                console.log(`oldIndex ${e["removed"]["oldIndex"]}`);
                this.oldIndex = e["removed"]["oldIndex"];
            }
        },
        handleDragEvent_SecondHalf(e) {
            if (Object.keys(e) == "added") {
                console.log(`${Object.keys(e)}`);
                console.log(`${Object.keys(e["added"])}`)
                console.log(`newIndex ${e["added"]["newIndex"]}`);
                console.log(`newIndex ${e["added"]["newIndex"] + 4}`);
                console.log(`${JSON.stringify(e["added"]["element"], null, 2)}`);
                // let findIdx = this.cpy_myArray.findIndex(({index})=>index==e["added"]["element"].index);
                // console.log('findIdx: ',findIdx);
                this.newIndex = e["added"]["newIndex"] + 4;

                // let tp = this.myArray[theNew];
            }

        },
        handleEnd: function (event) {
            if(this.isMoved_OneHalf){
                return false;
            }
            console.log(`${Object.keys(event)}`);
            let tp = this.cpy_myArray[this.newIndex];
            this.cpy_myArray[this.newIndex] = this.cpy_myArray[this.oldIndex];
            this.cpy_myArray[this.oldIndex] = tp;
            this.myArray = Object.assign(this.cpy_myArray);
            console.log(`end this.cpy_myArray: ${JSON.stringify(this.cpy_myArray, null, 2)}`);
        }
    },
    beforeMount() {
        for (let index = 1; index < 5; index++) {
            this.myArray.push({
                id: `cat_${index}`,
                name: `項目${index}`,
                class: `cat_${index}`
            })
        }
        for (let index = 1; index < 5; index++) {
            this.myArray.push({
                id: `spaceholder_${index}`,
                name: `項目${index}`,
                class: `spaceholder_${index}`
            })
        }
        this.cpy_myArray = Object.assign(this.myArray);
    },
    components: {
        Draggable
    },
    computed: {
        synValue: {
            get() {
                return this.goC
            },
            set(val) {
                this.$emit('update:goC', val);
            }
        }
    },
    watch: {
        myArray: function () {
            this.isMoved_OneHalf = false;
        }
    }
}

</script>
<style>
@import url('../css/DraggableLesson.css');
@import url('../css/page4/page4.css');
@import url('../css/PageStyle.css');
</style>