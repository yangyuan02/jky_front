<template>
    <div>
        <div class="data manage">
            <div class="table_header">
                <ul>
                    <li style="width:22%;">评价内容</li>
                    <li style="width:25%;">具体测评内容</li>
                    <li style="width:20.949%;">测评点</li>
                    <li style="width:7%;">状态</li>
                    <li style="width:7%">自评等级</li>
                    <li style="width:18.739%;">材料操作</li>
                </ul>
            </div>
            <div class="table_scroll" style="height:540px;width:1222px;margin:0 auto;overflow:scroll;">
                <table border="1" cellspacing="0">
                    <tr v-for="(item,index) in table" :key="index">
                        <td :rowspan="item.one_row" v-bind:class="{ show: item.show_one=='false'}" style="width:22%;">{{item.one.replace(/\s/g,"")}}</td>
                        <td :rowspan="item.two_row" v-bind:class="{ show: item.show_two=='false'}" style="width:25%;">{{item.two.replace(/\s/g,"")}}</td>
                        <td style="width:20.949%;">{{item.three.replace(/\s/g,"")}}</td>
                        <td style="width:7%;text-align:center;">
                            <i :class="item.status==1?'status1':'status2'"></i>
                        </td>
                        <td style="width:7%;text-align: center;">{{item.self_point}}</td>
                        <td style="width:18.739%;">
                            <a href="javascript:;" @click="goDatail(item.id)">上传</a>
                            <a href="javascript:;" @click="goDatail(item.id)">补传</a>
                        </td>
                    </tr>
                </table>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                table: [],
                point_count: {},
                progress: ''
            }
        },
        methods: {
            getData(url) { //获取数据
                this.$ajax.get(url, {}).then((res) => {
                    this.table = res.data
                }, (err) => {
                    console.log(err)
                })
            },
            getPoint_count() {
                this.$ajax.get('/api/role_points/point_count', {}).then((res) => {
                    this.progress = (res.data.finish / (res.data.finish + res.data.no_finish)) * 100 + '%'
                    this.point_count = res.data
                }, (err) => {
                    console.log(err)
                })
            },
            goDatail(id) { //跳转详情
                this.$router.push({
                    name: 'upload',
                    params: {
                        id: id
                    }
                })
            }
        },
        mounted() {
            this.getData('/api/role_points')
            this.getPoint_count()
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
    .manage .table_header {
        width: 1222px;
        margin: 0 auto;
    }
    .manage .table_header ul {
        display: flex;
        height: 52px;
        background: #2dc9b9;
        align-items: center;
        color: #fff;
    }
    .manage .table_header ul li {
        text-align: center;
    }
    .manage .table_body {
        width: 100%;
    }
    .manage table {
        width: 1222px;
        border: 1px solid #ccc;
        margin: 0 auto;
    }
    .manage table tr td:nth-child(6) {
        text-align: center;
    }
    .manage table tr td:nth-child(4) i.status1 {
        display: inline-block;
        width: 33px;
        height: 32px;
        background: url("../../assets/status1.png")
    }
    .manage table tr td:nth-child(4) i.status2 {
        display: inline-block;
        width: 33px;
        height: 32px;
        background: url("../../assets/status2.png")
    }
    .manage table tr td {
        padding: 4px 10px;
    }
    .manage table tr td:nth-child(6) a {
        color: #fff;
        background: #7acedf;
        width: 70px;
        height: 24px;
        line-height: 24px;
        text-align: center;
        display: inline-block;
        border-radius: 4px;
    }
    .manage table tr td:nth-child(6) a:last-child {
        background: #ccc;
    }
</style>

