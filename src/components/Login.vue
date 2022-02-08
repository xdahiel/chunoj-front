<template>
<div class="login_container">
  <div class="login_box">
    <div class="avatar_box">
      <img src="../assets/logo.png">
    </div>
    <el-form ref="loginFormRef" :model="loginForm" :rules="loginFormRules" label-width="0px" class="login_form">
      <el-form-item prop="Username">
        <el-input v-model="loginForm.Username" prefix-icon="el-icon-user"></el-input>
      </el-form-item>
      <el-form-item prop="Password">
        <el-input v-model="loginForm.Password" prefix-icon="el-icon-lock" type="password"></el-input>
      </el-form-item>
      <el-form-item class="btns">
        <el-button type="primary" @click="login">登录</el-button>
        <el-button type="primary">注册</el-button>
      </el-form-item>
    </el-form>
  </div>
</div>
</template>

<script>
export default {
  data () {
    return {
      loginForm: {
        Username: '',
        Password: ''
      },
      // 表单的验证规则
      loginFormRules: {
        Username: [
          { required: true, message: '请输入用户名', trigger: 'blur' },
          { min: 6, max: 20, message: '长度在 6 到 20 个字符', trigger: 'blur' }
        ],
        Password: [
          { required: true, message: '请输入密码', trigger: 'blur' },
          { min: 6, max: 20, message: '长度在 6 到 20 个字符', trigger: 'blur' }
        ]
      }
    }
  },
  methods: {
    login () {
      this.$refs.loginFormRef.validate(async (valid) => {
        if (!valid) return
        const { data: res } = await this.$http.post('login', this.loginForm)
        if (res.code !== '200') return console.log('登录失败')
        console.log('登录成功')
      })
    }
  }
}
</script>

<style lang="less" scoped>
.login_container {
  background: #2b4d6b;
  height: 100%;
}
.login_box {
  width: 450px;
  height: 300px;
  background: white;
  border-radius: 10px;
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
  .avatar_box {
    height: 130px;
    width: 130px;
    border: 1px solid #eee;
    border-radius: 50%;
    padding: 10px;
    box-shadow: 0 0 10px #ddd;
    position: absolute;
    left: 50%;
    transform: translate(-50%, -50%);
    background: #eee;
    img{
      width: 100%;
      height: 100%;
      border-radius: 50%;
      background: #eee;
    }
  }
}

.login_form {
  position: absolute;
  bottom: 0;
  width: 100%;
  padding: 0 20px;
  box-sizing: border-box;
}

.btns {
  display: flex;
  justify-content: center;
}
</style>
