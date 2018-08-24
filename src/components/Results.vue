<template>
  <div class="ip-calc-results" >
    <template v-if="cidr">
      <template v-for="cidrProp in cidrProps" >
        <div class="results-row" :key="cidrProp.key">
          <div class="results-cell key">
            {{cidrProp.name}}:
          </div>
          <div class="results-cell value">
            <!--
              For large masks lib returns something
              like 1.262177448353619e-29 which is
              unpleasant, so we round it to 0.
            -->
            <template v-if="cidrProp.key === 'numHosts'">
              {{Math.floor(cidr[cidrProp.key])}}
            </template>
            <template v-else-if="cidrProp.key === 'networkAddress'">
              {{`${cidr.networkAddress}/${cidr.subnetMaskLength}`}}
            </template>
            <template v-else>
              {{cidr[cidrProp.key]}}
            </template>
          </div>

        </div>
      </template>
    </template>
  </div>
</template>

<script>
import { cidrSubnet } from 'ip'

export default {
  name: 'Results',
  props: {
    request: String,
  },
  data: () => (
    {
      cidrProps: [
        { key: 'networkAddress', name: 'Network' },
        { key: 'firstAddress', name: 'First host' },
        { key: 'lastAddress', name: 'Last host' },
        { key: 'broadcastAddress', name: 'Broadcast' },
        // { key: 'subnetMaskLength', name: '' }, // 24 => 256
        { key: 'numHosts', name: 'Hosts' },
      ],
    }
  ),
  computed: {
    cidr: function () {
      try {
        // https://www.npmjs.com/package/ip
        return cidrSubnet(this.request)
      } catch (e) {
        return null
      }
    },
  },
}
</script>

<style scoped>
.ip-calc-results {
  display: table;
}

.results-row {
  display: table-row;
  text-align: left;
}

.results-cell {
  display: table-cell;
  padding: 2px 8px 2px 2px;
}

.results-cell.key {
  padding-left: 0.5em;
  color: #333;
}

.results-cell.value {
  font-weight: 500;
}
</style>
