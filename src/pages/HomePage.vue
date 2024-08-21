<script setup>
import { ref, watch } from 'vue';

// Define reactive variables for speed, time, and distance
const speed = ref(null);
const time = ref(null);
const distance = ref(null);

const calculateDistance = () => {
  if (speed.value !== null && time.value !== null) {
    distance.value = speed.value * time.value;
  }
};

const calculateTime = () => {
  if (speed.value !== null && distance.value !== null) {
    time.value = distance.value / speed.value;
  }
};

const calculateSpeed = () => {
  if (time.value !== null && distance.value !== null) {
    speed.value = distance.value / time.value;
  }
};

// Watchers to trigger calculation based on input changes
watch(speed, (newSpeed) => {
  if (newSpeed !== null) {
    calculateDistance();
    calculateTime();
  }
});

watch(time, (newTime) => {
  if (newTime !== null) {
    calculateDistance();
    calculateSpeed();
  }
});

watch(distance, (newDistance) => {
  if (newDistance !== null) {
    calculateSpeed();
    calculateTime();
  }
});
</script>

<template>
  <div>
    <input type="number" v-model="speed" placeholder="Enter speed">
    <input type="number" v-model="time" placeholder="Enter time">
    <input type="number" v-model="distance" placeholder="Enter distance">
    <p>Speed: {{ speed }}</p>
    <p>Time: {{ time }}</p>
    <p>Distance: {{ distance }}</p>
  </div>
</template>

<style scoped lang="scss">
/* Add your styles here */
</style>
