<template>
  <div v-if="course">
    <h3>Программа курса</h3>
    <ol>
      <li v-for="(item, index) in course.program" :key="index">
        {{ item }}
      </li>
    </ol>
  </div>
</template>

<script setup>
import { inject } from 'vue'

const course = inject('course')
</script>