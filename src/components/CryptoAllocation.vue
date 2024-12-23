<script setup lang="ts">
import { computed } from "vue";

const props = defineProps<{
  label: string;
  percentage: number;
  usd: number;
  rate: number;
}>();

const calculatedAllocation = computed(() => {
  // convert to percentage
  const percent = props.percentage * 0.01;

  console.log("Props: rate", props.rate, "usd", props.usd, "percent", percent);

  // return percent * props.usd;
  return percent * props.usd * props.rate;
});
</script>

<template>
  <div class="crypto-card">
    <label>{{ label }}</label>
    <input :value="calculatedAllocation" placeholder="" disabled />
  </div>
</template>

<style scoped>
.crypto-card {
  color: #000;
  display: flex;
  flex-direction: column;
}
</style>
