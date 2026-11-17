<template>
  <div class="page center">
    <h1>Личный кабинет</h1>
    <p>Вы авторизованы.</p>
    
    <button @click="logout" class="btn-danger">Выйти</button>
  </div>
</template>

<script setup>
import { useRouter } from 'vue-router'

const router = useRouter()

const logout = () => {
  localStorage.removeItem('authToken')
  router.push('/login')
}
</script>

<style scoped>
.center {
  text-align: center;
  margin-top: 3rem;
}
.btn-danger {
  padding: 0.5rem 1rem;
  background: #c62828;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  margin-top: 1rem;
}
.btn-danger:hover {
  background: #b71c1c;
}
</style>