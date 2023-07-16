<template>
    <div class="house-body">
        <div class="top">
            <el-button type="primary">
                新增绑定
            </el-button>
        </div>
        <div class="bottom">
            <div class="card" v-for="i in 16">
                <div class="card-top">
                    <div class="house-image">
                        <img src="http://127.0.0.1:32767/09.51.48/images/%E6%88%BF%E5%B1%8B%E7%AE%A1%E7%90%86/u9.png"/>
                    </div>
                    <div class="house-information">
                        <h2>祥源城</h2>
                        <h3>EA07栋-3单元-407室</h3>
                        <span>合肥市蜀山区银泰百货后面租金很贵的小区</span>
                        <p></p>
                        <li>身份：业主</li>
                        <li>面积：104m2</li>
                        <li>人口：3人</li>
                    </div>
                </div>
                <div class="card-bottom">
                    <el-button type="success" plain class="status-button">审核通过</el-button>
                    <el-button type="danger" plain class="delete-button">删除</el-button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: "house"
    }
</script>

<style scoped>
    img {
        height: 100%;
        width: 100%;
    }
    .house-body {
        display: flex;
        flex-direction: column;
        background-color: #eaeaea;
    }
    .top {
        padding: 20px;
    }
    .bottom {
        display: flex;
        flex-wrap: wrap;
        padding: 20px;
        justify-content: space-between;
    }
    .card {
        width: 400px;
        height: 300px;
        margin-bottom: 30px;
        display: flex;
        flex-direction: column;
        background-color: rgba(189, 189, 189, 0.48);
        box-shadow: 5px 5px 5px rgba(0, 0, 0, 0.2);
    }
    .card-top {
        flex: 2;
        display: flex;
    }
    .house-image {
        flex: 4;
    }
    .house-information {
        flex: 5;
        text-align: center;
    }
    .house-information li {
        font-size: 16px;
        color: #8b8b8b;
        list-style: none;
        line-height: 30px;
    }
    .card-bottom {
        flex: 1;
    }
    .status-button {
        position: relative;
        width: 150px;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        cursor: default;
    }
    .delete-button {
        position: relative;
        top: 50%;
        left: 50%;
        transform: translate(-60%, -50%);
    }
</style>