<template>
  <div class="page">
    <h1>Каталог курсов</h1>

    <div v-if="isLoading" class="spinner">
      Загрузка курсов...
    </div>

    <div v-else>
      <div class="filters">
        <button 
          :class="{ active: filter === 'all' }" 
          @click="setFilter('all')"
        >Все</button>
        <button 
          :class="{ active: filter === 'frontend' }" 
          @click="setFilter('frontend')"
        >Frontend</button>
        <button 
          :class="{ active: filter === 'backend' }" 
          @click="setFilter('backend')"
        >Backend</button>
      </div>

      <div class="course-list">
        <div v-for="course in filteredCourses" :key="course.id" class="course-card">
          <h3>{{ course.title }}</h3>
          <p>Категория: {{ course.category }}</p>
          
          <RouterLink :to="`/courses/${course.id}`" class="btn-more">
            Подробнее
          </RouterLink>
        </div>
      </div>
      
      <p v-if="filteredCourses.length === 0">Нет курсов в этой категории.</p>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue'
import { useRoute, useRouter } from 'vue-router'
import { courses } from '../data/courses'

const route = useRoute()
const router = useRouter()

const isLoading = ref(true)

const filter = computed(() => route.query.category || 'all')

onMounted(() => {
  setTimeout(() => {
    isLoading.value = false
  }, 1000)
})

const filteredCourses = computed(() => {
  if (filter.value === 'all') return courses
  return courses.filter(c => c.category === filter.value)
})

const setFilter = (value) => {
  router.push({ name: 'Courses', query: { category: value } })
}
</script>

<style scoped>
.filters {
  margin-bottom: 1rem;
}
.filters button {
  padding: 0.5rem 1rem;
  margin-right: 0.5rem;
  border: 1px solid #ccc;
  background: #fff;
  cursor: pointer;
  border-radius: 4px;
}
.filters button.active {
  background: #42b983;
  color: white;
  border-color: #42b983;
}
.course-list {
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
  margin-top: 1rem;
}
.course-card {
  border: 1px solid #eee;
  padding: 1rem;
  border-radius: 6px;
  width: 220px;
  box-shadow: 0 2px 4px rgba(0,0,0,0.05);
}
.course-card h3 {
  margin-top: 0;
  font-size: 1.1rem;
}
.course-card p {
  color: #666;
  font-size: 0.9rem;
}
.btn-more {
  display: inline-block;
  margin-top: 0.5rem;
  padding: 0.4rem 0.8rem;
  background: #42b983;
  color: white;
  text-decoration: none;
  border-radius: 4px;
  font-size: 0.9rem;
}
.btn-more:hover {
  background: #369c6c;
}
.spinner {
  margin-top: 2rem;
  font-size: 1.2rem;
  color: #42b983;
  font-weight: bold;
}
</style>