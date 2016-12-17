<template>
  <div id="app">

    <Midi></Midi>
  </div>
</template>

<script>
import Midi from './components/Midi'
export default {
  name: 'app',
  components: {
    Midi
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
