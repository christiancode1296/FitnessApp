<script setup>
  import {workoutProgram} from "../utils/index.js";

  const workoutTypes = ['Push', 'Pull', 'Legs']
</script>

<template>
  <section id="grid">
    <button :key="workoutId" v-for="(workout,workoutIdx) in Object.keys(workoutProgram)" class="card-button-plan-card">
      <div>
        <p>Day {{workoutIdx < 9 ? '0' + (workoutIdx + 1 ) : workoutIdx +1}}</p>
        <i class="fa-solid fa-dumbbell"></i>
        <i class="fa-solid fa-weight-hanging"></i>
        <i class="fa-solid fa-bolt"></i>
      </div>
      <h3>TYPES</h3>
    </button>
  </section>

</template>

<style scoped>

</style>