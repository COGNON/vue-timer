<script setup lang="ts">
import { computed } from 'vue';

const props = defineProps<{
  timeLimit: number;
  timePassed: number;
}>();

const SIZE = 500;
const XY = 250;
const R = XY - 10;
const STROKE = 2 * Math.PI * R;

const pathDash = computed(() => getPath(props.timeLimit, props.timePassed));
function getPath(limit: number, passed: number) {
  return (STROKE - getTimeFraction(limit, passed) * STROKE).toFixed(0);
}

function getTimeFraction(limit: number, passed: number) {
  const rawFraction = (limit - passed) / limit;
  return rawFraction - (1 / limit) * (1 - rawFraction);
}
</script>

<template>
  <svg class="t-timer-svg" :height="SIZE" :width="SIZE">
    <g class="t-timer-circle">
      <circle class="t-timer-path" :cx="XY" :cy="XY" :r="R" />

      <path
        :stroke-dasharray="`${pathDash} ${STROKE}`"
        :class="['t-timer-path-remaining']"
        :d="`M ${XY}, ${XY}
        m ${R}, 0
        a ${R}, ${R} 0 1,0 ${-(R * 2)},0
        a ${R}, ${R} 0 1,0 ${R * 2},0`"
      />
    </g>
  </svg>
</template>

<style lang="scss" scoped>
.t-timer-svg {
  transform: scaleX(-1);

  .t-timer-circle {
    fill: none;
    stroke: none;

    %path {
      stroke-width: 15px;
    }

    .t-timer-path {
      @extend %path;
      stroke: rgb(87, 87, 87);
    }

    .t-timer-path-remaining {
      @extend %path;
      stroke-linecap: round;
      transform: rotate(-90deg);
      transform-origin: center;
      transition: 1s linear all;
      stroke: #00cfbb;
    }
  }
}
</style>
