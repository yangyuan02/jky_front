<template>
    <div>
        <div class="data grade">
            <div class="grade_box">
                <div class="table_header">
                    <table border="1" cellspacing="0">
                        <tr>
                            <td :rowspan="3">评价内容</td>
                            <td :rowspan="3">具体测评内容</td>
                            <td :colspan="4">测评标准</td>
                        </tr>
                        <tr>
                            <td :rowspan="2">测评点</td>
                            <td :colspan="3">等级标准</td>
                        </tr>
                        <tr>
                            <td>A(完全落实)</td>
                            <td>B(基本落实)</td>
                            <td>C(明显不足或味落实)</td>
                        </tr>
                    </table>
                </div>
                <div class="table_body" style="height: 540px;margin: 0px auto; overflow: scroll;">
                    <table border="1" cellspacing="0">
                        <tr v-for="(item,index) in table" :key="index">
                            <td :rowspan="item.one_row" v-bind:class="{ show: item.show_one=='false'}">{{item.one.replace(/\s/g,"")}}</td>
                            <td :rowspan="item.two_row" v-bind:class="{ show: item.show_two=='false'}">{{item.two.replace(/\s/g,"")}}</td>
                            <td>{{item.three.replace(/\s/g,"")}}</td>
                            <td>{{item.a}}</td>
                            <td>{{item.b}}</td>
                            <td>{{item.c}}</td>
                        </tr>
                    </table>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                table: []
            }
        },
        methods: {
            getData(url) { //获取数据
                this.$ajax.get(url, {}).then((res) => {
                    this.table = res.data
                }, (err) => {
                    console.log(err)
                })
            }
        },
        mounted() {
            this.getData('/api/role_points')
        }
    }
</script>

<style>
    .show {
        display: none;
    }
    .data {
        background: #fff;
        margin: 0px 15px;
        box-shadow: 1px 1px 8px #ccc;
    }
    .grade .grade_box {
        width: 100%;
        height:auto;
        padding: 20px;
    }
    .grade .grade_box .table_header table {
        width: 100%;
        border: 1px solid #ccc;
    }
    .grade .grade_box .table_header table td {
        height: 30px;
        text-align: center;
        width:16.6%;
    }
    .grade .grade_box .table_body table td{
        width:16.6%;
    }
    .grade .grade_box .table_body table{
        border: 1px solid #ccc;
        border-top:none;
    }
</style>

