<script setup lang="ts">
defineProps<{ label: string }>();
</script>

<template>
  <button class="t-btn" role="button">{{ label }}</button>
</template>

<style lang="scss" scoped>
.t-btn {
  padding: 12px 24px;
  border: none;
  border-radius: 4px;
  background-color: var(--primary);
  color: var(--vt-c-white-mute);
  font-size: 16px;
  font-weight: 500;
  text-align: center;
  text-decoration: none;
  text-transform: uppercase;
  cursor: pointer;
  transition: background-color 0.2s ease-in-out;

  &:hover {
    background-color: var(--primary-highlight);
  }

  &:focus {
    outline: none;
    box-shadow: 0 0 0 3px var(--primary-shadow);
  }
}
</style>
