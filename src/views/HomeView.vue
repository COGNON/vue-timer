<script setup lang="ts">
import { ref, computed } from 'vue';
import TInput from '@/components/TInput.vue';
import TBtn from '@/components/TBtn.vue';
import TTimer from '@/components/TTimer.vue';
import TSvgTimer from '@/components/TSvgTimer.vue';

const timeInput = ref(5);
const timeLimit = computed(() => timeInput.value * 60); // max time in seconds
const timePassed = ref(0); // time in actual seconds

let timerEnd: number, timerCount: number;
function onStart() {
  if (!timeInput.value) return;

  timePassed.value = timeLimit.value - 1;
  timerCount = setInterval(onTimerCount, 1000);
  timerEnd = setTimeout(onTimerEnd, timeLimit.value * 1000);
}

function onTimerEnd() {
  timePassed.value = 0;
  clearTimeout(timerEnd);
  clearInterval(timerCount);
}

function onTimerCount() {
  timePassed.value -= 1;
}
</script>

<template>
  <div class="t-timer">
    <t-svg-timer :time-limit="timeLimit" :time-passed="timePassed" />

    <div class="t-timer-inputs column">
      <div class="row items-center t-gutter-x-sm">
        <t-input
          v-model.number="timeInput"
          @keyup.enter="onStart()"
          @update:model-value="timePassed = timeLimit"
        />
        <t-btn label="Start" @click.stop="onStart()" />
        <t-btn label="Stop" @click.stop="onTimerEnd()" />
      </div>
      <t-timer v-model="timePassed" />
    </div>
  </div>
</template>

<style lang="scss" scoped>
.t-timer {
  $size: 500px;
  height: $size;
  width: $size;
  position: relative;

  .t-timer-inputs {
    position: absolute;
    height: $size;
    width: $size;
    top: 0px;
    justify-content: center;
    align-items: center;
  }
}
</style>
