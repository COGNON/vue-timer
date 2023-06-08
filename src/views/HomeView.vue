<script setup lang="ts">
import { ref } from 'vue';
import TInput from '@/components/TInput.vue';
import TBtn from '@/components/TBtn.vue';

const timeInput = ref(5);
</script>

<template>
  <div class="row items-center t-gutter-x-sm">
    <t-input v-model="timeInput" label="Time" />
    <t-btn label="Start" />
  </div>
</template>
