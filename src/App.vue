<script setup>

import Welcome from "./components/pages/Welcome.vue";
import Layout from "./components/layouts/Layout.vue";
import Dashboard from "./components/pages/Dashboard.vue";
import Workout from "./components/pages/Workout.vue";
import {ref} from "vue";
import {workoutProgram} from "./utils/index.js";


const defaultData ={};
for (let workoutIdx in workoutProgram) {
  const workoutData = workoutProgram[workoutIdx];
  defaultData[workoutIdx] = {}
  for (let e of workoutData.workout) {
  defaultData[workoutIdx][e.name] = '';
  }
}

const selectedDisplay = ref(1);
const data = ref(defaultData);
const selectedWorkout = ref(-1);

function handleChangeDisplay(idx) {
  selectedDisplay.value = idx;
}
function handleSelectWorkout(idx) {
  selectedDisplay.value = 3;
  selectedWorkout.value = idx;
}
function handleSaveWorkout() {
  localstorage.setItem('workouts', JSON.stringify(data.value))

  selectedDisplay.value = 2;
  selectedWorkout.value = -1;


}
</script>

<template>
  <Layout>
    <!--     PAGE 1 -->
    <Welcome :handleChangeDisplay="handleChangeDisplay" v-if="selectedDisplay === 1"/>
    <!--    PAGE 2 -->
    <Dashboard v-if="selectedDisplay === 2"/>
    <!--    PAGE 3 -->
    <Workout :data="data" :selectedWorkout="selectedWorkout" v-if="workoutProgram?.[selectedWorkout]"/>
  </Layout>
</template>

<style scoped>

</style>
