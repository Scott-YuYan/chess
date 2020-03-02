<template>
    <div>
        <div class="center">
            <a href="http://plm2.xinri.com/Windchill/ptc1/document/create?ContainerOid=OR%3Awt.inf.library.WTLibrary%3A90945&u8=1&unique_page_number=58375170570698_0&AjaxEnabled=row&wizardActionClass=com.ptc.windchill.enterprise.doc.forms.CreateDocFormProcessor&wizardActionMethod=execute&tableID=table__folderbrowser_PDM_TABLE&actionName=create&portlet=poppedup&context=comp%24folderbrowser_table%24OR%3Awt.folder.Cabinet%3A90979%24&oid=OR%3Awt.folder.Cabinet%3A90979&CSRF_NONCE=EITVzpXdRDvClzGcJemUlOblAE6AwFnZVMyjhaLpD2G00QLGX7KNn8Klbw6mpwnmf8invNKlJwb4pgSkI7Xk%2BabpdQjxpgvvStKBg%2BfyChTy43DJacyUi6fkKUuDqgw%3D">新建文档</a>
            <button v-on:click="start">摇色子</button>
            <div v-if="a===1">
                <span>玩家1先走</span>
            </div>
            <div v-if="a===0">
                <span>玩家2先走</span>
            </div>
            <button v-bind:disabled="disabled1" v-on:click="player1">玩家1开始</button>
            <button v-bind:disabled="disabled2" v-on:click="start">玩家2开始</button>
        </div>
        <div class="center">
            <div class="chess">
                <div class="row">
                    <Cell v-on:mouseClick="getMessage(0,$event)" v-bind:n="n" v-bind:par1="par1" v-bind:par2="par2"
                          v-bind:finish="finish"/>
                    <Cell v-on:mouseClick="getMessage(1,$event)" v-bind:n="n" v-bind:par1="par1" v-bind:par2="par2"
                          v-bind:finish="finish"/>
                    <Cell v-on:mouseClick="getMessage(2,$event)" v-bind:n="n" v-bind:par1="par1" v-bind:par2="par2"
                          v-bind:finish="finish"/>
                </div>
                <div class="row">
                    <Cell v-on:mouseClick="getMessage(3,$event)" v-bind:n="n" v-bind:par1="par1" v-bind:par2="par2"
                          v-bind:finish="finish"/>
                    <Cell v-on:mouseClick="getMessage(4,$event)" v-bind:n="n" v-bind:par1="par1" v-bind:par2="par2"
                          v-bind:finish="finish"/>
                    <Cell v-on:mouseClick="getMessage(5,$event)" v-bind:n="n" v-bind:par1="par1" v-bind:par2="par2"
                          v-bind:finish="finish"/>
                </div>
                <div class="row">
                    <Cell v-on:mouseClick="getMessage(6,$event)" v-bind:n="n" v-bind:par1="par1" v-bind:par2="par2"
                          v-bind:finish="finish"/>
                    <Cell v-on:mouseClick="getMessage(7,$event)" v-bind:n="n" v-bind:par1="par1" v-bind:par2="par2"
                          v-bind:finish="finish"/>
                    <Cell v-on:mouseClick="getMessage(8,$event)" v-bind:n="n" v-bind:par1="par1" v-bind:par2="par2"
                          v-bind:finish="finish"/>
                </div>
                <div>
                    {{msg}}
                </div>
            </div>
        </div>
    </div>
</template>


<script>
    import Cell from "./components/Cell";

    export default {
        data() {
            return {
                n: 0, a: null, par1: 'O', par2: 'X',
                map: [[null, null, null], [null, null, null], [null, null, null]],
                msg: "游戏进行中...",
                finish: false,
                disabled1: true,
                disabled2: true
            };
        },
        components: {Cell},
        methods: {
            getMessage: function (num, text) {
                this.n += 1;
                this.map[Math.floor(num / 3)][num % 3] = text;
                this.result();
                console.log(`${num} is be button , content:${text}`);
            },
            result: function () {
                for (let i = 0; i < 3; i++) {
                    if ((this.map[i][0] != null) && (this.map[i][0] === this.map[i][1]) && (this.map[i][1] === this.map[i][2])) {
                        this.finish = true;
                        return this.msg = "游戏结束，" + this.map[i][0] + "胜利";
                    }
                }
                for (let j = 0; j < 3; j++) {
                    if ((this.map[0][j] != null) && (this.map[0][j] === this.map[1][j]) && this.map[1][j] === this.map[2][j]) {
                        this.finish = true;
                        return this.msg = "游戏结束，" + this.map[0][j] + "胜利";
                    }
                }
                if ((this.map[1][1] != null) && (this.map[0][0] === this.map[1][1]) && (this.map[1][1] === this.map[2][2])) {
                    this.finish = true;
                    return this.msg = "游戏结束，" + this.map[1][1] + "胜利";
                }
                if ((this.map[1][1] != null) && (this.map[0][2] === this.map[1][1]) && (this.map[1][1] === this.map[2][0])) {
                    this.finish = true;
                    return this.msg = "游戏结束，" + this.map[1][1] + "胜利";
                }
            },
            start: function () {
                this.a = (Math.floor(Math.random() * 10 + 1) % 2);
                if (this.a === 1) {
                    this.disabled1 = false;
                }
                if (this.a === 0) {
                    this.disabled2 = false;
                }
                console.log(this.a)
            },
            player1: function () {

                this.par1 = 'X';
                this.par2 = 'O';
            },
        }
    }
</script>

<style>
    .row {
        display: flex;
    }

    .center {
        display: flex;
        justify-content: center;
        align-items: center;
        flex-direction: column;
    }
</style>
