<template>
  <div class="m_content">
    <h3>智悦机器人交流论坛</h3>
    <div class="block">
<!--      <el-avatar :size="50" :src="user.avatar"></el-avatar>-->
      <div>{{user.username}}</div>
    </div>
    <div>
      <span><el-link href="/blogs">主页</el-link></span>
      <el-divider direction="vertical"></el-divider>
      <span><el-link type="success" href="/blog/add">发表博客</el-link></span>
      <el-divider direction="vertical"></el-divider>
      <span v-show="!hasLogin"><el-link href="/login">登录</el-link></span>
      <span v-show="hasLogin"><el-link type="danger" @click="logout">退出</el-link></span>
    </div>
  </div>
</template>

<script>
export default {
  name: "Header",
  data(){
    return{
      user:{
        username: '未登录',
      },
      hasLogin: false
    }
  },
  methods:{
    logout(){
      alert("退出成功")
      const _this = this
      _this.$axios.get("/logout",{
        headers: {
          "authentication": localStorage.getItem("token")
        }
      }).then(res =>{
        _this.$store.commit("REMOVE_INFO")
        _this.$router.push("/login")
      })
    }
  },
  created() {
    if(this.$store.getters.getUser.username){
      this.user.username = this.$store.getters.getUser.username
      this.user.avatar = this.$store.getters.getUser.avatar
      this.hasLogin = true
    }
  }
}
</script>

<style scoped>
.m_content{
  max-width: 960px;
  margin: 0 auto;
  text-align: center;
}
</style>