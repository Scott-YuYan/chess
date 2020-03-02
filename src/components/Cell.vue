<template>
    <div class="cell" v-on:click="init(par1,par2)">
        <template v-if="flag">{{text}}</template>
        <template v-else></template>
    </div>
</template>


<script>
    export default {
        props: ['n', 'par1', 'par2','finish'],
        data() {
            return {flag: false, text: " "}
        },
        computed: {
            // text() {
            //     return this.n % 2=== 0 ?"X":"O" ;
            // }
        },
        methods: {
            init: function (param1, param2) {
                if (this.flag) {
                    return;
                }
                console.log(this.finish);
                if (this.finish){
                    return;
                }

                this.text = this.n % 2 === 0 ? param1 : param2;
                this.$emit("mouseClick", this.text);
                this.flag = true;
            }
        }
    }
</script>

<style>
    .cell {
        border: 1px solid black;
        width: 50px;
        height: 50px;
        display: flex;
        justify-content: center;
        align-items: center;
        color: blue;
        font-size: 30px;
    }
</style>
