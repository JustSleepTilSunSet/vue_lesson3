<template>
    <!--D頁界標籤-->
    <div v-if="synValue">
 
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
        <!-- <draggable v-model="sysNameList" @start="drag = true"  @end="drag = false" group="people" class="bg_left">
            <div v-bind:class="element.class" v-for="element in sysNameList" :key="element.id" v-on:drag="handleDrag(element.replace)">{{ element.name }}</div>
        </draggable> -->
        <!-- <draggable class="backlog" v-model="spaceHolderList" group="people" @start="drag = true" @end="drag = false">
            <div v-bind:class="element.class" v-bind:hidden="false" v-for="element in spaceHolderList"
                :key="element.id">{{ element.name }}</div>
        </draggable> -->
        <!-- <draggable class="backlog" v-model="spaceHolderList" group="people" @start="drag=false" @end="drag=false">
            <div v-bind:class="element.class"  v-bind:hidden="false"  v-for="element in spaceHolderList" :key="element.id">{{ element.name }}</div>
        </draggable> -->
        <!-- </div> -->


        <!-- <div class="contents_bg">
        </div>
        <div class="nxt_btn" v-on:click="nextTriggerFun()">
            <div class="btn_content">
                上一頁
            </div>
        </div>

        <div class="page_content">
            這是C頁
        </div>
        <div>
            {{ this.isCurrShow }}
            <button> 下一頁 </button>
        </div> -->
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
            sysNameList: [],
            spaceHolderList: [],
            replaceMap: {},
            isCurrShow: this.goC,
            isDragedItem: null,
            spaceHolderListLen: 0
        }
    },
    methods: {
        nextTriggerFun: function () {
            console.log(`isShow in B: ${this.synValue}`);
            this.synValue = !this.synValue;
        },
        handleDrag(dragIndex){
            console.log(`this.isDragedItem: ${this.isDragedItem}`);
            this.isDragedItem = dragIndex;
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
        for (let index = 1; index <= 2; index++) {
            this.sysNameList.push({
                id: `cat_${index}`,
                replace: index,
                class: `cat_${index}`,
                name: `項目${index}`
            })
            this.replaceMap[index] = false;
        }

        for (let index = 1; index <= 2; index++) {
            this.sysNameList.push({
                id: index,
                class: `spaceholder`,
                name: `項目${index}`
            })
        }
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
        spaceHolderList: function () {
            console.log(`觸發了 ${JSON.stringify(this.spaceHolderList,null,2 )}`);
            if(this.isDragedItem != null){
                // const isLargeNumber = ({index}) => index == this.isDragedItem;
                // console.log(`value ${JSON.stringify(value,null,2)}`);
                // let findIdx = value.findIndex(value, isLargeNumber);
                // value[findIdx].class = `cat_${this.isDragedItem}`;
            }
            // console.log(JSON.stringify(this.spaceHolderList,null,2));
        }
    }
}
</script>

<style>
@import url('../css/Constants.css');
@import url('../css/PageStyle.css');
@import url('../css/page4/page4.css');
</style>