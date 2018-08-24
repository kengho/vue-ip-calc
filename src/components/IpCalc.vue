<template>
  <div class="ip-calc-wrapper">
    <div>
      <input
        autofocus
        class="request-input"
        placeholder="e.g. 192.168.0.0/24"
        v-on:input="request = $event.target.value"
      />
      <Results :request="request" />
    </div>
  </div>
</template>

<script>
import Results from './Results.vue'

export default {
  name: 'IpCalc',
  components: {
    Results,
  },
  data: function () {
    return {
      request: this.request,
    }
  },
}
</script>

<style scoped>

/* https://stackoverflow.com/a/6080482 */
input {
  font-family: inherit;
  font-size: inherit;
}

.ip-calc-wrapper {
  display: flex;
  justify-content: center;
}

.request-input {
  max-width: 16em;
}
</style>
