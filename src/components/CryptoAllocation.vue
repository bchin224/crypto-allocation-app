<script setup lang="ts">
import { computed } from "vue";

const props = defineProps<{
  label: string;
  percentage: number;
  usd: number;
  rate: number;
}>();

let cryptoAbrev = "";

const getCryptoAbreviation = (label: string) => {
  const abrevSplit = label.split(" ");
  cryptoAbrev = abrevSplit[0];
};

getCryptoAbreviation(props.label);

const calculatedAllocation = computed(() => {
  // convert to percentage
  const percent = props.percentage * 0.01;

  return percent * props.usd * props.rate;
});
</script>

<template>
  <div class="crypto-card">
    <label :for="cryptoAbrev" class="card-label">{{ label }}</label>
    <div class="input-wrapper">
      <input
        :id="cryptoAbrev"
        :value="calculatedAllocation"
        placeholder=""
        disabled
      />
      <!-- Display crypto icon -->
      <div
        class="icon-circle"
        :class="{
          'bitcoin-bg': cryptoAbrev === 'BTC',
          'ethereum-bg': cryptoAbrev === 'ETH',
        }"
      >
        <i
          class="fab"
          :class="cryptoAbrev === 'BTC' ? 'fa-btc' : 'fa-ethereum'"
          :alt="cryptoAbrev === 'BTC' ? 'Bitcoin' : 'Ethereum'"
        ></i>
      </div>
    </div>
    <div class="exchange-rate-footer">
      ^The current USD exchange rate for {{ cryptoAbrev }} is {{ rate }}
    </div>
  </div>
</template>

<style scoped>
.crypto-card {
  color: #000;
  display: flex;
  flex-direction: column;
  background: #2765f8;
  border-radius: 10px;
  margin: 10px;
  padding: 10px;
}
.card-label {
  font-weight: 600;
  color: #fff;
}
.input-wrapper {
  position: relative;
  display: flex;
  align-items: center;
}
.icon {
  position: absolute;
  right: 1rem;
  font-size: 1rem;
}
.fab:before {
  color: #fff;
}
.bitcoin-bg {
  background-color: #f7931a;
}
.ethereum-bg {
  background-color: #6375de;
}
.exchange-rate-footer {
  color: #fff;
  font-size: 0.75em;
}
</style>
