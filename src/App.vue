<script setup>

import Welcome from "./components/pages/Welcome.vue";
import Layout from "./components/layouts/Layout.vue";
import Dashboard from "./components/pages/Dashboard.vue";
import Workout from "./components/pages/Workout.vue";
import {computed, ref} from "vue";
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

const istWorkoutComplete = computed(() => {
  const currWorkout= data.value?.[selectedWorkout.value];
  if (!currWorkout) {return false}

  const isCompleteCheck =Object.values(currWorkout).every(ex => !!ex)
  console.log('ISCOMPLETE: ', isCompleteCheck)
  return isCompleteCheck
  })

const firstIncompleteWorkoutIndex = computed(() => {
  const allWorkouts = data.value
  if(!allWorkouts) {return -1}

  for (const [index, workout] of Object.entries(allWorkouts)) {
    const isComplete = Object.values(workout).every(ex => !!ex)
    if(!isComplete) {
      console.log('First incomplete workout index:', parseInt(index))
      return parseInt(index)
    }
  }
  console.log('All workouts complete, returning -1')
  return -1;
})


function handleChangeDisplay(idx) {
  selectedDisplay.value = idx;
}
function handleSelectWorkout(idx) {
  console.log('handleSelectWorkout called with idx:', idx)
  console.log('Setting selectedDisplay to 3')
  selectedDisplay.value = 3;
  selectedWorkout.value = idx;
  console.log('selectedDisplay:', selectedDisplay.value, 'selectedWorkout:', selectedWorkout.value)
}
function handleSaveWorkout() {
  localStorage.setItem('workouts', JSON.stringify(data.value))

  selectedDisplay.value = 2;
  selectedWorkout.value = -1;

  function handleResetPlan() {
    selectedDisplay.value = 2
    selectedWorkout.value = -1
    data.value = defaultData
    localStorage.removeItem('workouts')
  }

}
</script>

<template>
  <Layout>
    <!--     PAGE 1 -->
    <Welcome :handleChangeDisplay="handleChangeDisplay" v-if="selectedDisplay === 1"/>
    <!--    PAGE 2 -->
    <Dashboard :firstIncompleteWorkoutIndex="firstIncompleteWorkoutIndex" :handleSelectWorkout="handleSelectWorkout" v-if="selectedDisplay === 2"/>
    <!--    PAGE 3 -->
    <Workout :handleSaveWorkout="handleSaveWorkout" :isWorkoutComplete="istWorkoutComplete"  :data="data" :selectedWorkout="selectedWorkout" v-if="selectedDisplay === 3"/>
  </Layout>
</template>

<style scoped>

</style>
