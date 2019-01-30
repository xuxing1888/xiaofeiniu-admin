<template>
  <div id="app">
    <!--h3>{{1000 | date}}</h3>
    <h3>{{1000 | datetime}}</h3>
    <h3>{{1000 | currency}}</h3-->
    <router-view/>
    <!--全局配置： {{$store.state.globalSettings}}-->
  </div>
</template>

<script>
  export default {
    mounted(){
      //当前组件挂载完成后需要异步请求全局设置
      var url= this.$store.state.globalSettings.apiUrl+'/admin/settings';
      this.$axios.get(url).then((res)=>{
        //将全局配置存储到Vuex存储仓库
        this.$store.commit('setGlobalSettings',res.data);
      }).catch((err)=>{
        console.log(err);
      })
    }
  }
</script>

<style lang="scss">
#app {
  font-family: "Helvetica Neue",Helvetica,"PingFang SC","Hiragino Sans GB","Microsoft YaHei","微软雅黑",Arial,sans-serif;
  color: #303133;       
}
</style>
