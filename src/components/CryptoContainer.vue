<script setup lang="ts">
import CryptoAllocation from "./CryptoAllocation.vue";
</script>

<template>
  <div class="card container">
    <h2>Crypto Allocations</h2>
    <CryptoAllocation label="BTC Allocation (70%)" :percentage="70" />
    <CryptoAllocation label="ETH Allocation (30%)" :percentage="30" />
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
