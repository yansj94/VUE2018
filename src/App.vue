<template>
  <div id="app">
    <img src="./assets/logo.png">
    <HelloWorld/>
    <FDG/>
    <myFDG/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld'
import FDG from './components/FDG'
import myFDG from './components/myFDG'
export default {
  name: 'App',
  components: {
    HelloWorld,
    FDG,
    myFDG
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
