<template>
  <div id="app">

    <router-view/>
    <!--<router-link to="/a">跳转</router-link>-->
  </div>
</template>

<script>
  // import A from './components/bossActive.vue'
  export default {
    name: 'App',
    data(){
      return{
        webTitle:"招募合伙人"
      }
    }
  }
</script>

<style>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    /*text-align: center;*/
    color: #2c3e50;
  }
body{
  margin: 0;
}
</style>
