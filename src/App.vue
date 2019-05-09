<template>
  <div id="app">
    <HealthBar/>
    <img src="./assets/logo.png">
    <HealthBar/>
  </div>
</template>

<script>
import HealthBar from './components/HealthBar'
import Button from './components/Button'

export default {
  name: 'App',
  components: {
    HealthBar,
    Button
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
