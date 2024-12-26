<script setup lang="ts">
import CryptoAllocation from "./CryptoAllocation.vue";
import { ref, onMounted, onUnmounted } from "vue";

const btcRate = ref(0);
const ethRate = ref(0);
let readableTimestamp = "";

const fetchRates = async () => {
  try {
    const response = await fetch(
      "https://api.coinbase.com/v2/exchange-rates?currency=USD"
    );
    const data = await response.json();
    btcRate.value = parseFloat(data.data.rates.BTC); // Convert to number
    ethRate.value = parseFloat(data.data.rates.ETH); // Convert to number
    // console.log("BTC Rate:", btcRate.value);
    // console.log("ETH Rate:", ethRate.value);
    const timestamp = new Date().toISOString();

    readableTimestamp = new Date(timestamp).toLocaleString("en-US", {
      year: "numeric",
      month: "long",
      day: "numeric",
      hour: "2-digit",
      minute: "2-digit",
      second: "2-digit",
      hour12: true,
    });
  } catch (error) {
    console.error("Fetch error:", error);
  }
};

let intervalId: ReturnType<typeof setInterval>;

onMounted(() => {
  fetchRates(); // Fetch immediately on component mount
  intervalId = setInterval(fetchRates, 15000); // Refresh every 15 seconds
});

onUnmounted(() => {
  clearInterval(intervalId); // clear interval when the component is unmounted
});

defineProps<{ usd: number }>();
</script>

<template>
  <div class="card container">
    <h2>Crypto Allocations</h2>
    <div class="last-refresh">
      *Rates last updated at {{ readableTimestamp }}
    </div>
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
.container {
  border: 1px solid #969696;
  background: #eee;
}
.last-refresh {
  font-size: small;
}
</style>
