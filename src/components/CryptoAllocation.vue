<script setup lang="ts">
import { computed } from "vue";

const props = defineProps<{
  label: string;
  percentage: number;
  usd: number;
  rate: number;
}>();

const calculatedAllocation = computed(() => {
  return props.usd * props.rate;
});

console.log("Props: rate", props.rate, "usd", props.usd);
</script>

<template>
  <div class="crypto-card">
    <label>{{ label }}</label>
    <input :value="calculatedAllocation" placeholder="" disabled />
    <!-- <input :value="usd" placeholder="" disabled /> -->
  </div>
</template>

<style scoped>
.crypto-card {
  color: #000;
  display: flex;
  flex-direction: column;
}
</style>
