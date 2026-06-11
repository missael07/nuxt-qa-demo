<script setup lang="ts">
const email = ref('')
const password = ref('')
const error = ref('')

function login() {
  error.value = ''

  if (!email.value || !password.value) {
    error.value = 'Email and password are required.'
    return
  }

  const savedEmail = localStorage.getItem('qa_user_email')
  const savedPassword = localStorage.getItem('qa_user_password')

  if (email.value !== savedEmail || password.value !== savedPassword) {
    error.value = 'Invalid credentials.'
    return
  }

  localStorage.setItem('qa_logged_in', 'true')
  navigateTo('/dashboard')
}
</script>

<template>
  <main class="container">
    <h1>Login</h1>

    <p v-if="error" class="error" data-testid="error-message">{{ error }}</p>

    <form data-testid="login-form" @submit.prevent="login">
      <div class="form-group">
        <label for="email">Email</label>
        <input id="email" name="email" type="email" v-model="email" />
      </div>

      <div class="form-group">
        <label for="password">Password</label>
        <input id="password" name="password" type="password" v-model="password" />
      </div>

      <button type="submit">Login</button>
    </form>

    <p>No account? <NuxtLink to="/register">Register</NuxtLink></p>
  </main>
</template>
