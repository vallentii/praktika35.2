<template>
  <div class="page center">
    <h1>404</h1>
    <h2>Страница не найдена</h2>
    <RouterLink to="/" class="btn-home">На главную</RouterLink>
  </div>
</template>

<style scoped>
.center {
  text-align: center;
  margin-top: 3rem;
}
.btn-home {
  display: inline-block;
  margin-top: 1rem;
  padding: 0.5rem 1rem;
  background: #42b983;
  color: white;
  text-decoration: none;
  border-radius: 4px;
}
.btn-home:hover {
  background: #369c6c;
}
</style>