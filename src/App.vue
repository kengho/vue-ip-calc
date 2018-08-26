<template>
  <div id="app">
    <IpCalc />
    <GithubMark
      href="https://github.com/kengho/vue-ip-calc"
      position="bottom-right"
    />
  </div>
</template>

<script>
import GithubMark from 'vue-github-mark'
import IpCalc from './components/IpCalc.vue'

export default {
  name: 'app',
  components: {
    IpCalc,
    GithubMark,
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
