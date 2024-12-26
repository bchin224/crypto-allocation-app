<script setup lang="ts">
defineProps<{ label: string; usd: number }>();
const usd = defineModel<number>("usd", { required: true });
const emit = defineEmits(["update:usd"]); // Define custom event to be emitted to parent component

// Validate input to only numbers
const validateInput = (event: Event) => {
  const input = (event.target as HTMLInputElement).value;
  const numericValue = parseFloat(input);

  if (!isNaN(numericValue)) {
    emit("update:usd", numericValue); // Emit the valid value back to the parent
  } else {
    emit("update:usd", 0);
  }

  // Regex allowing numbers and decimal point
  (event.target as HTMLInputElement).value = input
    .replace(/[^0-9.]/g, "")
    .replace(/(\..*)\./g, "$1");
};
</script>

<template>
  <div class="input-card card">
    <h2>Investable Assets</h2>
    <label for="usd-input">{{ label }}</label>
    <div class="input-wrapper">
      <input
        id="usd-input"
        :value="usd"
        @input="validateInput"
        placeholder="Insert USD here"
      />
      <div class="icon-circle">
        <i class="fas fa-dollar-sign icon" alt="USD"></i>
      </div>
    </div>
  </div>
</template>

<style scoped>
.input-card {
  color: #000;
  display: flex;
  flex-direction: column;
  margin-bottom: 15px;
  border: 1px solid #969696;
  background: #eee;
  height: 100%;
}
.input-wrapper {
  position: relative;
  display: flex;
  align-items: center;
}
.icon {
  position: absolute;
  font-size: 1rem;
  color: #fff;
}
.icon-circle {
  background-color: #008a26;
}
.icon-circle i {
  font-size: 1rem;
}
</style>
