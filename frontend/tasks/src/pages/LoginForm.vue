<script setup lang="ts">
import { ref } from 'vue'
import { useRouter } from 'vue-router'

const username = ref('')
const password = ref('')
const router = useRouter()

const login = () => {
  if (username.value === 'admin' && password.value === 'admin123') {
    localStorage.setItem('auth', 'true')
    router.push('/tarefas')
  } else {
    alert('Credenciais inválidas')
  }
}
</script>

<template>
  <div class="login-page">
    <h1 class="login-title">Task Manager</h1>

    <div class="login-container">
      <form @submit.prevent="login" class="login-form">
        <div class="input-group">
          <label for="username">Usuário</label>
          <input type="text" id="username" v-model="username" required />
        </div>
        <div class="input-group">
          <label for="password">Senha</label>
          <input type="password" id="password" v-model="password" required />
        </div>
        <button type="submit" class="login-button">Entrar</button>
      </form>
    </div>
  </div>
</template>

<style scoped>
.login-page {
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0 5vw;
  background-color: #121212;
  height: 600px;
  overflow: hidden;
}

.login-title {
  font-size: 2.5rem;
  font-weight: bold;
  color: #f0f0f0;
}

.login-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.login-form {
  max-width: 400px;
  width: 100%;
  background: #000000;
  padding: 2rem;
  border-radius: 12px;
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.3);
}

.input-group {
  margin-bottom: 1.5rem;
  display: flex;
  flex-direction: column;
}

.input-group label {
  margin-bottom: 0.5rem;
  font-size: 0.95rem;
  color: #ccc;
}

.input-group input {
  padding: 0.75rem 1rem;
  border: none;
  border-radius: 8px;
  background-color: #3a3a3a;
  color: #f0f0f0;
  font-size: 1rem;
}

.input-group input:focus {
  outline: 2px solid #42b983;
  background-color: #444;
}

.login-button {
  width: 100%;
  padding: 0.75rem;
  font-size: 1.1rem;
  font-weight: bold;
  color: white;
  background-color: #42b983;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  transition: background 0.3s ease;
}

.login-button:hover {
  background-color: #369b6f;
}
</style>