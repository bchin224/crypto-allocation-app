<script setup lang="ts">
// import { ref } from "vue";

defineProps<{ label: string; percentage: number }>();
</script>

<template>
  <div class="crypto-card">
    <label>{{ label }}</label>
    <input placeholder="" disabled />
  </div>
</template>

<style scoped>
.crypto-card {
  color: #000;
  display: flex;
  flex-direction: column;
}
</style>
