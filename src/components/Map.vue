<template>
  <v-row align="center" justify="center">
    <v-col cols="3">
      <h2 class="text-h5 font-weight-bold">{{ name }}</h2>
    </v-col>

    <v-col cols="3">
      <h2 :class="{'text-h6 font-weight-bold': true, 'green-text': soloCountdown < 180}" align="center">{{ formatTime(soloCountdown) }}</h2>
    </v-col>

    <v-col cols="3">
      <h2 :class="{'text-h6 font-weight-bold': true, 'green-text': duoCountdown < 180}" align="center">{{ formatTime(duoCountdown) }}</h2>
    </v-col>

    <v-col cols="3">
      <h2 :class="{'text-h6 font-weight-bold': true, 'green-text': trioCountdown < 180}" align="center">{{ formatTime(trioCountdown) }}</h2>
    </v-col>
  </v-row>
</template>

<script setup lang="ts">
import { defineProps, ref, onMounted, onBeforeUnmount } from 'vue';

const props = defineProps({
  name: {
    type: String,
    required: true
  },
  startTime: {
    type: Number,
    required: true
  }
});

const soloCountdown = ref(0);
const duoCountdown = ref(0);
const trioCountdown = ref(0);
const currentTimeSeconds = new Date().getTime() / 1000;

const formatTime = (seconds: number): string => {
  const mins = Math.floor(seconds / 60);
  const secs = (seconds % 60).toFixed(0);
  return `${mins.toString().padStart(1, '0')}:${secs.toString().padStart(2, '0')}`;
};

const calculateCountdowns = () => {
  const now = Math.floor(performance.now() / 1000);
  const startOfDay = Math.floor(new Date().setUTCHours(0, 0, 0, 0) / 1000);
  const elapsed = (now + currentTimeSeconds + props.startTime - startOfDay - 1) % 540; // 540 seconds = 9 minutes

  soloCountdown.value = (540 - elapsed) % 540;
  duoCountdown.value = (540 - elapsed + 180) % 540;
  trioCountdown.value = (540 - elapsed + 360) % 540;
};

onMounted(() => {
  calculateCountdowns();
  const interval = setInterval(() => {
    calculateCountdowns();
  }, 1000);
  onBeforeUnmount(() => clearInterval(interval));
});
</script>

<style scoped>
.green-text {
  color: green;
}
</style>
