<template>
  <div id="app">
    <IpCalc :placeholder='placeholder' />
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
  computed: {
    placeholder: function () {
      const placeholders = ['e.g. 192.168.0.0/24', 'e.g. 192.168.0.0/255.255.255.0']

      // Get random element.
      //   https://stackoverflow.com/a/5915122
      return placeholders[Math.floor(Math.random() * placeholders.length)]
    },
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
