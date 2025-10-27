<script setup>
  import {workoutProgram} from "../utils/index.js";

  const workoutTypes = ['Push', 'Pull', 'Legs']
</script>

<template>
  <section id="grid">
    <button :key="workoutIdx" v-for="(workout,workoutIdx) in Object.keys(workoutProgram)" class="card-button-plan-card">
      <div>
        <p>Day {{workoutIdx < 9 ? '0' + (workoutIdx + 1 ) : workoutIdx +1}}</p>
        <i class="fa-solid fa-dumbbell" v-if="workoutIdx % 3 === 0"></i>
        <i class="fa-solid fa-weight-hanging" v-if="workoutIdx % 3 === 1"></i>
        <i class="fa-solid fa-bolt" v-if="workoutIdx % 3 === 2"></i>
      </div>
      <h3>{{ workoutTypes[workoutIdx % 3]}}</h3>
    </button>
  </section>

</template>

<style scoped>

</style>