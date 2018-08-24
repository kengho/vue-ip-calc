<template>
  <div id="app">
    <IpCalc />
  </div>
</template>

<script>
import IpCalc from './components/IpCalc.vue'

export default {
  name: 'app',
  components: {
    IpCalc,
  },
  created() {
    document.title = "IP Calc";
  },
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  font-size: 18px;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  margin-top: 32px;
}
</style>
