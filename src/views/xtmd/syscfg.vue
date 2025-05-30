<template>
        <div>
                <hr style=" border-color: #000000;">
                <el-row>
                        <el-col :span="12">
                                <!-- 第一行第一列 -->
                                <el-card shadow="hover" class="box-card1 ">
                                        <div class="welcome" style="color: lightcoral; font-size: 13px;">
                                                <span> 欢迎使用商品进销存管理系统 </span> <br>
                                                <span>&emsp;springboot,mybatis,SpringSecurity,mysql,vue <br>
                                                        完善的认证授权</span>
                                        </div>
                                </el-card>
                                <el-card shadow="hover" class="box-card2 " style=" box-shadow: 0 0px 0px 0 rgba(0, 0, 0, 0.0) ">
                                        <span>当前的登陆用户是:</span>
                                        <span style="color: rgb(237, 24, 24); font-size: 20px;">{{ this.adminName }}</span>
                                </el-card>

                        </el-col>
                        <!-- 第一行第二列 -->
                        <el-col :span="12">
                                <el-card shadow="hover" class="box-card1 ">
                                        <span style="font-size: 25px;">商品进销存管理系统</span>
                                        <div style="color: blueviolet; font-size: 13px;">
                                                <span>&emsp;系统是为完成本科毕设而设计开发的,功能大部分是完善的,<br>
                                                        可以作为一个学习springBoot框架以及vue的简单模板。<br>
                                                        并且可以扩展引入其他的技术框架比如 redis等</span>
                                        </div>
                                </el-card>
                        </el-col>
                </el-row>

                <el-row>
                        <el-col  :span="6">
                                <el-card shadow="hover" class="box-card2 " style=" box-shadow: 0 0px 0px 0 rgba(0, 0, 0, 0.0) ">
                                                <span style="font-size: 20px;">技术交流请添加微信</span><br><br> 
                                                <img src="@/assets/images/WeChat.jpg" style="width: 250px; height: 250px; margin-left: 200px;"> 
                                </el-card>
                        </el-col>
                </el-row>
        </div>
</template>

<script>

export default {
        data() {
                return {
                        adminName: sessionStorage.getItem('username'),
                }
        }
}
</script>
<style lang='less' scoped>

.el-card{
        border: none;
}
.el-row {
        margin-bottom: 20px;

        &:last-child {
                margin-bottom: 0;
        }
}

.el-col {
        margin-top: 12px;
}

.box-card1 {
        width: 500px;
        margin-left: 0%;

        .welcome {
                //   margin-top: 100px;
                font-size: 16px;
        }

        .margin-top {
                font-size: 30px;
                // margin-top: 40px;
        }
}

//第二个框
.box-card2 {
        margin-top: 0%;
        width: 500px;
        // margin-left: 50%;

        .margin-top {
                font-size: 30px;
                margin-top: 20px;
        }
}
</style>