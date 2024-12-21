<script setup lang="ts">
import InvestableInput from "./components/InvestableInput.vue";
import CryptoContainer from "./components/CryptoContainer.vue";
</script>

<template>
  <div class="card main-app">
    <InvestableInput label="Investable Assets" />
    <CryptoContainer />
  </div>
</template>

<style scoped>
.main-app {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  width: 100%;
}
.main-app > * {
  max-width: calc(50% - 16px);
}
@media (max-width: 560px) {
  .main-app > * {
    flex: 1 1 100%;
    max-width: 100%;
  }
}
</style>
