<template>
  <div class="login_container">
    <div class="login_form">
      <p class="login_title">商品进销存管理系统</p>
      <el-form :model="form" :rules="rules" status-icon label-width="100px" class="demo-ruleForm" ref="formName">
        <el-form-item label="账号" prop="username">
          <el-input v-model="form.username" placeholder="请输入账号"></el-input>
        </el-form-item>
        <el-form-item label="密码" prop="password">
          <el-input type="password" v-model="form.password" show-password placeholder="请输入密码"></el-input>
        </el-form-item>

        <el-form-item>
          <el-button type="primary" size="medium" @click="submitFormData">登录</el-button>
        </el-form-item>
      </el-form>
    </div>
  </div>
</template>
<script>
export default {
  name: "Login",
  data() {
    return {
      form: {
        username: "",
        password: "",
      },
      rules: {
        username: [{ required: true, message: "请输入账号", trigger: "blur" }],
        password: [{ required: true, message: "请输入密码", trigger: "blur" }],
      },
      rules: {
        username: [{ required: true, message: "请输入账号", trigger: "blur" }],
        password: [{ required: true, message: "请输入密码", trigger: "blur" }],
      },
    };
  }, methods: {
    // 提交登录表单的数据
    submitFormData() {
      // console.log(this.form);
      this.$refs['formName'].validate((valid) => {
        if (valid) {
          this.$http.post("/login", this.form)
            .then((res) => {
              // console.log(res);
              //获取服务端返回的信息
              if (res.data.code === 200) {
                // 表示登录成功
                // 1.存储相关的token信息  token信息在响应的header中
                sessionStorage.setItem("token", res.headers.authorization)
                sessionStorage.setItem("username", this.form.username)
                // 2.路由到主页面  --路由中配置了重定向
                this.$router.push("/")
              } else {
                // 表示登录失败，显示错误提示
                this.$message.error(res.data.msg+"或者新员工未分配角色");
              }
            });
        } else {
          return false;
        }
      });
    }
  }
}
</script>
<style lang="less" scoped>
.login_container {
  width: 100%;
  height: 100vh;
  background-color: rgba(242, 242, 242, 1);
  background-image: url(../assets/images/login_bg.jpg);
  background-size: auto;
  background-position: center bottom;
  background-repeat: no-repeat;
  background-size: 1278px 559px;
 
  border: none;
  border-radius: 0px;
  display: flex;
  justify-content: center;
  align-items: center;

  .login_form {
    width: 510px;
    margin: 0px auto;
    padding: 0 55px 15px 35px;
    background-color: #fff;
    border: none;
    border-radius: 5px;
    // 添加阴影效果
    box-shadow: 0 0 25px #cac6c6;

    .login_title {
      font-family: "微软雅黑 Bold", "微软雅黑";
      font-weight: 700;
      text-decoration: none;
      color: rgb(0, 121, 254);
      font-size: 32px;
      margin-top: 50px;
      margin-bottom: 30px;
      text-align: center;
    }
  }
}
</style>