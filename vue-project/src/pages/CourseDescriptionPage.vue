<template>
  <div v-if="course">
    <h3>Описание курса</h3>
    <p>{{ course.description }}</p>
  </div>
</template>

<script setup>
import { inject } from 'vue'

const course = inject('course')
</script>