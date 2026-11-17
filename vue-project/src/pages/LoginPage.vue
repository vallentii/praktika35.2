<template>
  <div class="page center">
    <h2>Вход в систему</h2>
    
    <form @submit.prevent="login">
      <input 
        v-model="password" 
        type="password" 
        placeholder="Введите пароль (1234)" 
      />
      <button type="submit">Войти</button>
    </form>
    
    <p v-if="error" class="error">{{ error }}</p>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter, useRoute } from 'vue-router'

const password = ref('')
const error = ref(null)
const router = useRouter()
const route = useRoute()

const login = () => {
  error.value = null
  if (password.value === '1234') {
    localStorage.setItem('authToken', 'demo')
    const redirectPath = route.query.redirect || '/dashboard'
    router.push(redirectPath)
  } else {
    error.value = 'Неверный пароль. Попробуйте "1234"'
  }
}
</script>

<style scoped>
.center {
  text-align: center;
  margin-top: 3rem;
}
input {
  padding: 0.5rem;
  margin-right: 0.5rem;
  border: 1px solid #ccc;
  border-radius: 4px;
}
button {
  padding: 0.5rem 1rem;
  background: #42b983;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}
.error {
  color: red;
  margin-top: 0.5rem;
}
</style>
