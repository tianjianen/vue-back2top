<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
    <HelloWorld msg="Welcome to Your Vue.js App"/>
    <HelloWorld msg="Welcome to Your Vue.js App"/>
    <Back2Top/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
// import Back2Top from './components/index'
import Back2Top from 'k-vue-back2top'

export default {
  name: 'app',
  components: {
    HelloWorld,
    Back2Top
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
