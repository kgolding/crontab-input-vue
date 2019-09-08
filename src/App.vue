<template>
  <div id="app">
    <h1>CrontabInput</h1>

  <div style="width: 600px;">
    <CrontabInput :value="value"></CrontabInput>
  </div>
  <br>
  <div>
    Value: <input type="text" v-model="value">
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
