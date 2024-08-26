<script setup>
import { ref } from 'vue';

// Initialize variables with default values
const selectedCalculation = ref('');
const speed = ref(0);
const time = ref(0);
const distance = ref(0);

// Calculation function with robust checks and initializations
const calculate = () => {
  console.log('Calculating:', selectedCalculation.value);
  if (selectedCalculation.value === 'speed' && time.value !== 0 && distance.value !== 0) {
    speed.value = distance.value / time.value;
  } else if (selectedCalculation.value === 'time' && speed.value !== 0 && distance.value !== 0) {
    time.value = distance.value / speed.value;
  } else if (selectedCalculation.value === 'distance' && speed.value !== 0 && time.value !== 0) {
    distance.value = speed.value * time.value;
  }
};
</script>

<template>
  <div>
    <h2>Select a Calculation:</h2>
    <button @click="selectedCalculation = 'speed'">Calculate Speed</button>
    <button @click="selectedCalculation = 'time'">Calculate Time</button>
    <button @click="selectedCalculation = 'distance'">Calculate Distance</button>

    <div v-if="selectedCalculation">
      <h3>Enter Values:</h3>

      <div v-if="selectedCalculation === 'speed'">
        <input required min="1" type="number" v-model.number="distance" placeholder="Enter distance" />
        <input required min="1" type="number" v-model.number="time" placeholder="Enter time" />
      </div>

      <div v-if="selectedCalculation === 'time'">
        <input required min="1" type="number" v-model.number="speed" placeholder="Enter speed" />
        <input required min="1" type="number" v-model.number="distance" placeholder="Enter distance" />
      </div>

      <div v-if="selectedCalculation === 'distance'">
        <input required min="1" type="number" v-model.number="speed" placeholder="Enter speed" />
        <input required min="1" type="number" v-model.number="time" placeholder="Enter time" />
      </div>

      <button @click="calculate">Calculate</button>

      <!-- Conditional Rendering of Results -->
      <div v-if="selectedCalculation === 'speed' && speed !== 0">
        <p>Calculated Speed: {{ speed }} m/p</p>
      </div>
      <div v-if="selectedCalculation === 'time' && time !== 0">
        <p>Calculated Time: {{ time }} hours</p>
      </div>
      <div v-if="selectedCalculation === 'distance' && distance !== 0">
        <p>Calculated Distance: {{ distance }} Miles</p>
      </div>
    </div>
  </div>
</template>

<style scoped>
button {
  margin: 0.5em;
}

input {
  display: block;
  margin: 1em 0;
}
</style>
