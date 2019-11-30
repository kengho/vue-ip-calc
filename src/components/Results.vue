<template>
  <div class="ip-calc-results">
    <template v-if="networkData">
      <template v-for="networkProp in this.networkProps">
        <div class="results-row" :key="networkProp.key">
          <div class="results-cell key">
            {{networkProp.name}}:
          </div>
          <div class="results-cell value">
            <!--
              For large masks lib returns something
              like 1.262177448353619e-29 which is
              unpleasant, so we round it to 0.
            -->
            <template v-if="networkProp.key === 'numHosts'">
              {{Math.floor(networkData.numHosts)}}
            </template>
            <template v-else-if="networkProp.key === 'networkAddress'">
              {{`${networkData.networkAddress}/${networkData.subnetMaskLength}`}}
            </template>
            <template v-else>
              {{networkData[networkProp.key]}}
            </template>
          </div>
        </div>
      </template>
    </template>
  </div>
</template>

<script>
import { cidrSubnet, subnet } from 'ip'

export default {
  name: 'Results',
  props: {
    request: String,
  },
  data: () => (
    {
      networkProps: [
        { key: 'networkAddress', name: 'Network' },
        { key: 'subnetMask', name: 'Subnet mask' },
        { key: 'firstAddress', name: 'First host' },
        { key: 'lastAddress', name: 'Last host' },
        { key: 'broadcastAddress', name: 'Broadcast' },
        // { key: 'subnetMaskLength', name: '' }, // 24 => 256
        { key: 'numHosts', name: 'Hosts' },
      ],
    }
  ),
  computed: {
    networkData: function () {
      if (!this.request) {
        return null
      }

      let result
      const matchCidr = this.request.match(/^\d+\.\d+\.\d+\.\d+\/\d+$/)
      if (matchCidr) {
        try {
          // https://www.npmjs.com/package/ip
          result = cidrSubnet(this.request)
        } catch (e) {
          // TODO: print error.
        }
      } else {
        const matchDotted = this.request.match(/^(\d+\.\d+\.\d+\.\d+)\/(\d+\.\d+\.\d+\.\d+)$/)
        if (matchDotted) {
          const address = matchDotted[1]
          const netmask = matchDotted[2]
          try {
            result = subnet(address, netmask)
          } catch (e) {
            // TODO: print error.
          }
        }
      }

      return result
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
