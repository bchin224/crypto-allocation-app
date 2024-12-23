<script setup lang="ts">
defineProps<{ label: string; percentage: number; usd: number; rate: number }>();
</script>

<template>
  <div class="crypto-card">
    <label>{{ label }}</label>
    <input :value="usd" placeholder="" disabled />
  </div>
</template>

<style scoped>
.crypto-card {
  color: #000;
  display: flex;
  flex-direction: column;
}
</style>
