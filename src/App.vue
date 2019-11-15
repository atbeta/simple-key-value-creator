<template>
  <div id="app">
    <config-item />
  </div>
</template>

<script>
import ConfigItem from './components/config-item'

export default {
  name: 'app',
  components: {
    ConfigItem
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
