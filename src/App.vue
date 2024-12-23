<script setup lang="ts">
import InvestableInput from "./components/InvestableInput.vue";
import CryptoContainer from "./components/CryptoContainer.vue";
import { ref } from "vue";

const usd = ref(0);
</script>

<template>
  <div class="card main-app">
    <InvestableInput label="Investable Assets" v-model:usd="usd" />
    <CryptoContainer :usd="usd" />
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
