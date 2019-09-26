<template>
  <el-container class="index">
    <el-header>
      <div class="logo">
        <img src="../assets/logo.png" alt />
      </div>
      <div class="title">
        <h2>电商后台管理系统</h2>
      </div>
      <div class="logout">
        欢迎光临~
        <a @click="logout" href="JavaScript:;">退出</a>
      </div>
    </el-header>
    <el-container>
      <el-aside width="200px">
        <el-menu
          default-active="2-2"
          class="el-menu-vertical-demo"
          background-color="#545c64"
          text-color="#fff"
          active-text-color="#ffd04b"
          unique-opened
        >
          <el-submenu index="1">
            <template slot="title">
              <i class="el-icon-location"></i>
              <span>用户管理</span>
            </template>
            <el-menu-item index="1-1">
              <i class="el-icon-menu"></i>
              <span slot="title">用户列表</span>
            </el-menu-item>
          </el-submenu>
          <el-submenu index="2">
            <template slot="title">
              <i class="el-icon-location"></i>
              <span>权限管理</span>
            </template>
            <el-menu-item index="2-1">
              <i class="el-icon-menu"></i>
              <span slot="title">角色列表</span>
            </el-menu-item>
            <el-menu-item index="2-2">
              <i class="el-icon-menu"></i>
              <span slot="title">权限列表</span>
            </el-menu-item>
          </el-submenu>
        </el-menu>

      </el-aside>
      <el-main>主体</el-main>
    </el-container>
  </el-container>
</template>

<script>
export default {
  methods: {
    logout () {
      this.$confirm('你确认要退出吗?', '温馨提示', {
        type: 'warning'
      })
        .then(() => {
          localStorage.removeItem('token')
          this.$router.push('/login')
          this.$message.success('退出成功')
        })
        .catch(e => {
          console.log('取消')
        })
    }
  }
}
</script>

<style lang='scss' scoped >
//默认情况下,单页应用程序中,不同组件的样式不会互相影响
.index {
  height: 100%;
  .el-header {
    background-color: #d8d8d8;
    display: flex;
    .logo {
      width: 180px;
      padding: 10px;
      img {
        height: 40px;
      }
    }
    .title {
      flex: 1;
      h2 {
        text-align: center;
        line-height: 60px;
        color: #545c64;
      }
    }
    .logout {
      width: 180px;
      line-height: 60px;
      text-align: right;
      float: right;
      a {
        color: orange;
        font-weight: 700;
      }
    }
  }
  .el-aside {
    background-color: #545c64;
    .el-menu{
      border-right:none;
    }
  }
  .el-main {
    background-color: #ecf0f1;
  }
}
</style>
