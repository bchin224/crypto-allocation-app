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
console.log(cryptoAbrev + "_input");

const calculatedAllocation = computed(() => {
  // convert to percentage
  const percent = props.percentage * 0.01;

  // console.log("Props: rate", props.rate, "usd", props.usd, "percent", percent);

  return percent * props.usd * props.rate;
});
</script>

<template>
  <div class="crypto-card">
    <label :for="cryptoAbrev">{{ label }}</label>
    <input
      :id="cryptoAbrev"
      :value="calculatedAllocation"
      placeholder=""
      disabled
    />
    <div class="exchange-rate-footer">
      The current USD exchange rate for {{ cryptoAbrev }} is {{ rate }}
    </div>
  </div>
</template>

<style scoped>
.crypto-card {
  color: #000;
  display: flex;
  flex-direction: column;
}
.exchange-rate-footer {
  font-size: 0.75em;
}
</style>
