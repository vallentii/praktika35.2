<template>
  <div class="page" v-if="course">
    <h1>{{ course.title }}</h1>
    <p>Категория: {{ course.category }}</p>

    <nav class="tabs">
      <RouterLink to="description" class="tab">Описание</RouterLink>
      <RouterLink to="program" class="tab">Программа</RouterLink>
      <RouterLink to="reviews" class="tab">Отзывы</RouterLink>
    </nav>

    <div class="tab-content">
      <RouterView />
    </div>

    <RouterLink to="/courses" class="btn-back">← Назад к списку</RouterLink>
  </div>

  <div class="page" v-else>
    <h2>Курс не найден</h2>
    <p>Возможно, он был удален или вы ввели неверный ID.</p>
    <RouterLink to="/courses" class="btn-back">← Назад к списку</RouterLink>
  </div>
</template>

<script setup>
import { computed, provide } from 'vue'
import { courses } from '../data/courses'

const props = defineProps({
  id: { type: [String, Number], required: true }
})

const course = computed(() => {
  return courses.find(c => c.id === Number(props.id))
})
provide('course', course)
</script>

<style scoped>
.tabs {
  margin: 1.5rem 0;
  border-bottom: 1px solid #ccc;
}
.tab {
  padding: 0.5rem 1rem;
  text-decoration: none;
  color: #666;
  display: inline-block;
}
.tab.router-link-active {
  border-bottom: 2px solid #42b983;
  color: #42b983;
  font-weight: bold;
}
.tab-content {
  padding: 1rem 0;
  min-height: 100px;
}
.btn-back {
  display: inline-block;
  margin-top: 1rem;
  color: #42b983;
  text-decoration: none;
}
.btn-back:hover {
  text-decoration: underline;
}
</style>