<script setup lang="ts">
const value = defineModel<number>({ default: 5 });
const NAME = 't-input';

defineProps<{ label?: string; width?: number | string }>();
</script>

<template>
  <div class="t-input column">
    <input
      v-model="value"
      type="number"
      min="1"
      :name="NAME"
      placeholder=" "
      :style="{ width: `${width || 80}px` }"
    />
    <label v-if="label" :for="NAME">{{ label }}</label>
  </div>
</template>

<style lang="scss" scoped>
.t-input {
  $color: var(--vt-c-white-mute);

  position: relative;

  %general {
    color: $color;
    transition: all 0.2s ease-out;
    font-size: 1.2rem;
  }

  label {
    @extend %general;
    position: absolute;
    top: 0px;
    left: 0px;
    transform-origin: top left;
    pointer-events: none;
    padding: 5px;
  }

  $border-color: var(--primary);
  input {
    @extend %general;
    background-color: transparent;
    border: none;
    border-bottom: 2px solid #7d7d7d;
    padding: 10px;
    outline: none;
  }

  input:focus {
    border-color: $border-color;
  }

  input:focus + label,
  input:not(:placeholder-shown) + label {
    font-size: 14px;
    color: $border-color;
    transform: translateY(-30px);
  }
}
</style>
