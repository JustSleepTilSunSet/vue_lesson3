<template>
    <div v-show="true">
        <img v-if = "!isNext" src="../assets/PageA/progressbar.png" class="process_bar_1">
        <div v-if = "!isNext" class="contents_bg"></div>
        <div v-if = "!isNext" class="nxt_btn" v-on:click="nextTriggerFun()">
            <div class="btn_content">
                開始任務
            </div>
        </div>

        <div v-if = "!isNext" class="page_content">
            勇者！歡迎來到TT資訊王國，我是TT King
            在正式加入王國的敏捷騎士團以前，需要請你先了解騎士團的Scrum流程與精神
                    
            請跟隨我一起通過Scrum新手村的挑戰任務吧！ 這是A頁
        </div>
        <div v-if = "!isNext" class="itme1"></div>

        <PageB v-bind:isNext.sync="isNext"></PageB>
    </div>
</template>
<script>
import PageB from './PageB.vue';

export default {
    data() {
        return {
            isNext: false
        }
    },
    beforeMount(){
        console.log(`isNext ${this.isNext}`);
    },
    methods: {
        nextTriggerFun: function(){
            this.isNext = !this.isNext;
            console.log(`isNext觸發!! ${this.isNext}`);
        }
    },
    components:{
        PageB
    }
}
</script>

<style>
@import url('../css/Constants.css');
@import url('../css/PageStyle.css');
@import url('../css/page1/Page1.css');

</style>