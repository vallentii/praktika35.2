<template>
  <div v-if="course">
    <h3>Отзывы студентов</h3>

    <div v-if="course.reviews.length > 0">
      <div v-for="(review, index) in course.reviews" :key="index" class="review">
        <strong>{{ review.author }}</strong> (Оценка: {{ review.rating }}/5)
        <p>{{ review.text }}</p>
      </div>
    </div>
    
    <p v-else>Пока нет отзывов на этот курс.</p>
  </div>
</template>

<script setup>
import { inject } from 'vue'

const course = inject('course')
</script>

<style scoped>
.review {
  margin-bottom: 1rem;
  padding-bottom: 0.5rem;
  border-bottom: 1px solid #eee;
}
.review p {
  margin-top: 0.5rem;
  color: #333;
}
</style>