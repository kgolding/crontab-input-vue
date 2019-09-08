<template>
  <div id="app">
    <h1>CrontabInput</h1>

  <div style="border: solid 1px lime;">
    <CrontabInput :value="value"></CrontabInput>
  </div>
  <div>
    Value: {{ value }}
  </div>

  </div>
</template>

<script>
import CrontabInput from './components/CrontabInput'

export default {
  name: 'app',
  data: function () {
    return {
      value: "* * * * * *"
    }
  },
  components: {
    CrontabInput
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
