<script setup lang="ts">
// import { ref } from "vue";

defineProps<{ label: string }>();
const usd = defineModel();

// const assets = ref(0);
</script>

<template>
  <div class="input-card">
    <h2>Asset Allocation Calculator</h2>
    <label>{{ label }}</label>
    <input placeholder="Insert USD here" v-model="usd" />
  </div>
</template>

<style scoped>
.input-card {
  color: #000;
  display: flex;
  flex-direction: column;
  margin-bottom: 15px;
}
</style>
