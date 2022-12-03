<template>
    <div v-if="goB">
        <img v-if="!goC" class="process_bar_2" src="../assets/PageB/progressbar2.png">
        <div v-if="!goC" class="contents_bg"></div>
        <div v-if="!goC" class="previous_page" v-on:click="nextTriggerFun()">
            <div v-if="!goC" class="btn_content">
                上一頁
            </div>
        </div>
        <div v-if="!goC" class="arrow_big_default" v-on:click="nextPageFun()">
        </div>
        <div v-if="!goC" class="page_content">
            我是TT資訊王國．敏捷騎士團的軍師小敏 用你們的話來說就是PO，
            也就是產品負責人 Product Owner PO會負責評估產品代辦清單的價值與重要性，
            依序排列要執行的優先順序，對齊產品目標，最後排出產品待辦清單 Product Backlog。
        </div>
        <div v-if="!goC" class="itme2">
        </div>
        <PageC v-bind:goC.sync="goC"></PageC>
    </div>
</template>
<script>
import PageC from './PageC.vue';
export default {
    props: ["isNext"],
    data() {
        return {
            isCurrShow: this.isNext,
            goC: false
        }
    },
    methods: {
        nextTriggerFun: function () {
            console.log(`isShow in B: ${this.goB}`);
            this.goB = !this.goB;
        },
        nextPageFun: function () {
            console.log(`isShow in B: ${this.goB}`);
            this.goC = !this.goC;
        }
    },
    components: {
        PageC
    },
    computed: {
        goB: {
            get() {
                return this.isNext
            },
            set(val) {
                this.$emit('update:isNext', val);
            }
        }
    }
}
</script>

<style>
@import url('../css/Constants.css');
@import url('../css/PageStyle.css');
@import url('../css/page2/page2.css');
</style>