<script setup lang="ts">
import CryptoAllocation from "./CryptoAllocation.vue";
import { ref } from "vue";

// make api call every 5 seconds to provide real time updates
const result = ref(null);
const btcRate = ref(0);
const ethRate = ref(0);

fetch("https://api.coinbase.com/v2/exchange-rates?currency=USD")
  .then((response) => response.json())
  .then((data) => {
    result.value = data;
    btcRate.value = Number(data.data.rates.BTC); // Access the Bitcoin rate
    ethRate.value = Number(data.data.rates.ETH); // Access the Ethereum rate
    console.log("BTC Rate:", btcRate.value);
    console.log("ETH Rate:", ethRate.value);
  })
  .catch((error) => console.error("Fetch error:", error));

defineProps<{ usd: number }>();
</script>

<template>
  <div class="card container">
    <h2>Crypto Allocations</h2>
    <CryptoAllocation
      label="BTC Allocation (70%)"
      :percentage="70"
      :usd="usd"
      :rate="btcRate"
    />
    <CryptoAllocation
      label="ETH Allocation (30%)"
      :percentage="30"
      :usd="usd"
      :rate="ethRate"
    />
  </div>
</template>

<style scoped>
h2 {
  margin: 0px;
  color: #000;
}
.container {
  border: 1px solid #969696;
  background: #eee;
}
</style>
