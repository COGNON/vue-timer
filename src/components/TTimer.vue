<script setup lang="ts">
import { computed } from 'vue';

const displayActualNumber = defineModel({ default: 0 });

const displayValue = computed(() => {
  const minutes = Math.floor(displayActualNumber.value / 60);
  const seconds = displayActualNumber.value - minutes * 60;
  return padStart(String(minutes), 2, '0') + ':' + padStart(String(seconds), 2, '0');
});

function padStart(str: string, len: number, fill: string): string {
  if (str.length < len) {
    const padNum = len - str.length;
    return fill.repeat(padNum) + str;
  }
  return str;
}
</script>

<template>
  <p class="t-timer-text">{{ displayValue }}</p>
</template>

<style scoped>
.t-timer-text {
  font-size: 5rem;
}
</style>
