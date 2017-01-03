<template>
  <div id="app">
    <!--<h1><i class="cloud icon"></i></h1>-->
    <home></home>
  </div>
</template>

<script>
import Home from './components/Home'

export default {
  name: 'app',
  components: {
    Home
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 100px;
}
#app .h1 {
  margin: 0 auto;
  text-align: center !important;
}
.cloud {
  font-size: 5em !important;
  color: #276F86;
}
</style>
