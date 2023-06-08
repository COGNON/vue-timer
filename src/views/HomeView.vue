<script setup lang="ts">
import { ref } from 'vue';
import TInput from '@/components/TInput.vue';
import TBtn from '@/components/TBtn.vue';
import TTimer from '@/components/TTimer.vue';

const timeInput = ref(5);
const displayActualNumber = ref(0); // time in actual seconds

let timerEnd: number, timerCount: number;
function onStart() {
  if (!timeInput.value) return;

  displayActualNumber.value = timeInput.value * 60;

  timerEnd = setTimeout(onTimerEnd, timeInput.value * 60 * 1000);
  timerCount = setInterval(onTimerCount, 1000);
}

function onTimerEnd() {
  displayActualNumber.value = 0;
  clearTimeout(timerEnd);
  clearInterval(timerCount);
}

function onTimerCount() {
  displayActualNumber.value -= 1;
}
</script>

<template>
  <div class="t-input-wrapper row items-center t-gutter-x-sm">
    <t-input v-model.number="timeInput" label="Time" @keyup.enter="onStart()" />
    <t-btn label="Start" @click.stop="onStart()" />
    <t-btn label="Stop" @click.stop="onTimerEnd()" />
  </div>

  <t-timer v-if="displayActualNumber" v-model="displayActualNumber" />
</template>
