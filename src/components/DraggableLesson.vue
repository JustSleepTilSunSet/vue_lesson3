<template>
    <div>
        <h3>{{ msg }}</h3>
        <!-- <draggable class="item" v-model="myArray" @change="handleDragEvent_SecondHalf($event)" group="people" @start="drag = true"
            @end="drag = false">
            <div class="item_setting" v-for="element in myArray.slice(0, 5)" :key="element.id">{{ element.name }}
            </div>
        </draggable> -->

        <draggable class="bg_left" v-model='myArray' @change="handleDragEvent_OneHalf($event)" group="people"
            @start="drag = true" @end="handleEnd($event)">
            <div v-bind:class="element.class" v-for="element in myArray.slice(0, 4)" :key="element.class">{{ element.content }}
            </div>
        </draggable>

        <draggable class="backlog" v-model='myArray' @change="handleDragEvent_OneHalf($event)" group="people"
            @start="drag = true" @end="handleEnd($event)">
            <div v-bind:class="element.class" v-for="element in myArray.slice(4, 9)" :key="element.class">{{ element.content }}
            </div>
        </draggable>
        <!-- <draggable class="backlog" v-model="myArray" @change="handleDragEvent_SecondHalf($event)" group="people"
            @start="drag = true" @end="handleEnd($event)">
            <div v-bind:class="element.class" v-for="element in myArray.slice(4, 9)" :key="element.class">
                {{ element.content }}
            </div>
        </draggable> -->
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
            newIndex: 0,
            isMoved_OneHalf:false,
            isMoved_SecondHalf:false,
            spaceContent: ["優先度最高", "優先度高", "優先中", "優先低"],
            catContent: ["會員系統 (登入、註冊、權限管理)", "應徵者的線上履歷編輯器", "前台職缺列表 (職缺詳情、點擊應徵)", "後台職缺管理功能 (資訊上架下架、應徵者資料)"]
        }
    },
    beforeMount() {
        for (let index = 1; index < 5; index++) {
            this.myArray.push({
                id: `cat_${index} cat_content${index}`,
                name: `項目${index}`,
                class: `cat_${index} cat_content${index}`,
                content:this.catContent.shift()
            })
        }

        for (let index = 1; index < 5; index++) {
            this.myArray.push({
                id: `spaceholder_${index}  sapceholder_content${index}`,
                name: `項目${index}`,
                class: `spaceholder_${index}  sapceholder_content${index}`,
                content:this.spaceContent.shift()
            })
        }
        console.log(`this.myArray: ${this.myArray.length}`);
        this.cpy_myArray = Object.assign(this.myArray);
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
                this.myArray[this.oldIndex].class = `spaceholder_1  sapceholder_content1`;
            }
        },
        handleDragEvent_SecondHalf(e) {
            this.isMoved_SecondHalf = Object.keys(e)=="moved"; 
            console.log(`this.isMoved_SecondHalf isMove ${this.isMoved_SecondHalf}`);
            console.log(`${JSON.stringify(this.myArray,null,2)}`);
            if (Object.keys(e) == "added") {
                console.log(`${Object.keys(e)}`);
                console.log(`${Object.keys(e["added"])}`)
                console.log(`newIndex ${e["added"]["newIndex"]}`);
                console.log(`newIndex ${e["added"]["newIndex"] + 3}`);
                console.log(`${JSON.stringify(e["added"]["element"], null, 2)}`);
                this.newIndex = e["added"]["newIndex"] + 3;
                // let tp = this.myArray[theNew];
            }

        },
        handleEnd: function (event) {
            if(this.isMoved_OneHalf){
                return false;
            }
            if(this.isMoved_SecondHalf){
                return false;
            }
            console.log(`${Object.keys(event)}`);
            let tp = this.cpy_myArray[this.newIndex];
            this.cpy_myArray[this.newIndex] = this.cpy_myArray[this.oldIndex];
            this.cpy_myArray[this.oldIndex] = tp;
            this.myArray = Object.assign(this.cpy_myArray);
        }
    },
    components: {
        Draggable
    },
    computed: {
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
</style>