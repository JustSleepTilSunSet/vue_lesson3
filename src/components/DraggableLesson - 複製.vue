<template>
    <div>
        <h3>{{ msg }}</h3>
        <!-- <draggable class="item" v-model="myArray" @change="handleDragEvent_SecondHalf($event)" group="people" @start="drag = true"
            @end="drag = false">
            <div class="item_setting" v-for="element in myArray.slice(0, 5)" :key="element.id">{{ element.name }}
            </div>
        </draggable> -->

        <draggable class="item" v-model='myArray' @change="handleDragEvent_OneHalf($event)" group="people"
            @start="drag = true" @end="handleEnd()">
            <div class="item_setting" v-for="element in myArray.slice(0, 5)" :key="element.id">{{ element.name }}
            </div>
        </draggable>

        <draggable class="item" v-model="myArray" @change="handleDragEvent_SecondHalf($event)" group="people"
            @start="drag = true" @end="drag = false">
            <div class="item_setting" v-for="element in myArray.slice(5, 10)" :key="element.id">{{ element.name }}
            </div>
        </draggable>
        <!-- <button v-on:click="testing">hh</button> -->
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
            myArray: [],
            cpy_myArray: [],
            oldIndex: 0,
            newIndex: 0
        }
    },
    methods: {
        finish: function (item) {
            console.log(item.moved.element) // { id: 1, name: 'Item 1' }
        },
        handleDragEvent_OneHalf(e) {
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
        handleEnd: function () {
            let tp = this.cpy_myArray[this.newIndex];
            this.cpy_myArray[this.newIndex] = this.cpy_myArray[this.oldIndex];
            this.cpy_myArray[this.oldIndex] = tp;
            this.myArray = Object.assign(this.cpy_myArray);
            console.log(`end this.cpy_myArray: ${JSON.stringify(this.cpy_myArray, null, 2)}`);
        }
    },
    beforeMount() {
        for (let index = 1; index <= 5; index++) {
            this.myArray.push({
                id: index,
                name: `項目${index}`
            })
        }
        for (let index = 6; index <= 10; index++) {
            this.myArray.push({
                id: index,
                name: `項目${index}`
            })
        }
        this.cpy_myArray = Object.assign(this.myArray);
        // console.log(JSON.stringify(this.myArray, null, 2));
    },
    components: {
        Draggable
    },
    computed: {
    },
    watch: {
        myArray: function () {
            // let tp = this.cpy_myArray[this.newIndex];
            // this.cpy_myArray[this.newIndex] = this.cpy_myArray[this.oldIndex];
            // this.cpy_myArray[this.oldIndex] = tp;
            // this.myArray = Object.assign(this.cpy_myArray);
            // console.log(`this.cpy_myArray: ${JSON.stringify(this.cpy_myArray, null, 2)}`);
        }
    }
}

</script>
<style>
@import url('../css/DraggableLesson.css');
</style>