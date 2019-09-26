<template>
  <div class="login">
    <el-form :model="form" :rules="rules" label-width="80px" status-icon ref='form'>
      <img class="logo" src="../assets/avatar.jpg" alt="">
      <el-form-item label="用户名" prop="username">
        <el-input placeholder="请输入用户名" v-model="form.username"></el-input>
      </el-form-item>
      <el-form-item label="密  码" prop="password">
        <el-input placeholder="请输入密码" type="password" v-model="form.password"></el-input>
      </el-form-item>
      <el-form-item>
        <el-button @click="login" class="loginBtn" type="primary">登录</el-button>
        <el-button @click="reset">重置</el-button>
      </el-form-item>
    </el-form>
  </div>
</template>

<script>
import axios from 'axios'
// 导出的是组件配置对象,除了template其它都能配
// 组件定义的规范:定义的组件的根元素上,一般有一个组件同名的类名
// 定义的是login组件=>根元素上就要有.login类
export default {
  data () {
    return {
      form: {
        username: '',
        password: ''
      },
      // 配置校验规则
      // required:true  表示必填项
      // message :提示信息
      // trigger: 触发校验,blur失去焦点时候的校验
      // trigger: change值改变的时候触发校验
      // status-icon 配置表单校验反馈的图标
      // 通过ref和$refs可以获取到元素和或者组件
      rules: {
        username: [
          { required: true, message: '请输入用户名', trigger: ['blur', 'change'] },
          { min: 3, max: 12, message: '用户名必须是3-12个字符', trigger: ['blur', 'change'] }
        ],
        password: [
          { required: true, message: '请输入密码', trigger: ['blur', 'change'] },
          { min: 6, max: 12, message: '密码必须是6-12个字符', trigger: ['blur', 'change'] }
        ]
      }
    }
  },
  methods: {
    reset () {
      this.$refs.form.resetFields()
    },
    login () {
      this.$refs.form.validate(isValid => {
        if (!isValid) return
        // axios({
        //   method: 'post',
        //   url: 'http://localhost:8888/api/private/v1/login',
        //   data: this.form
        // }).then(res => {
        //   // console.log(res.data)
        //   const { meta } = res.data
        //   if (meta.status === 200) {
        //     console.log('登录成功')
        //   } else {
        //     console.log(meta.msg)
        //   }
        // })

        // axios 优化
        // axios.请求方式('请求地址',请求参数).then(res=>{})
        axios.post('http://localhost:8888/api/private/v1/login', this.form).then(res => {
          const { meta, data } = res.data
          if (meta.status === 200) {
            localStorage.setItem('token', data.token)

            this.$message.success('登录成功')

            // this.$router整个路由实例,可以有个方法,push方法,可以跳转路由
            // this.$route 当前路由相关信息

            this.$router.push('/index')
          } else {
            this.$message({
              type: 'error',
              message: meta.msg,
              duration: 1000
            })
          }
        })
      })
    }
  }
}
</script>

<style lang="scss" scoped>
.login {
  background-color: #2d234c;
  width: 100%;
  height: 100%;
  overflow: hidden;

  .el-form {
    background-color: #fff;
    width: 400px;
    padding: 20px;
    padding-top: 70px;
    margin: 0 auto;
    margin-top: 200px;
    border-radius:20px;
    position: relative;

    .logo{
      position: absolute;
      top: 0;
      left: 50%;
      transform: translate(-50%,-50%);
      border-radius:50%;
      width: 80px;
      height: 80px;
      border: 5px solid #fff;

    }
    .loginBtn{
      margin-right: 80px;
    }
  }
}
</style>
