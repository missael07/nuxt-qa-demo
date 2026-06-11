<script setup>
import { ref } from 'vue'

const email = ref('')
const password = ref('')
const confirmPassword = ref('')
const error = ref('')
const success = ref('')

async function register() {
  error.value = ''
  success.value = ''

  if (!email.value || !password.value || !confirmPassword.value) {
    error.value = 'All fields are required.'
    return
  }

  if (!email.value.includes('@')) {
    error.value = 'Email is invalid.'
    return
  }

  if (password.value.length < 8) {
    error.value = 'Password must be at least 8 characters.'
    return
  }

  if (password.value !== confirmPassword.value) {
    error.value = 'Passwords do not match.'
    return
  }

  localStorage.setItem('qa_user_email', email.value)
  localStorage.setItem('qa_user_password', password.value)

  success.value = 'Account created successfully.'

  await navigateTo('/login')
}
</script>

<template>
  <main class="container">
    <h1>Register</h1>

    <p v-if="error" class="error" data-testid="error-message">{{ error }}</p>
    <p v-if="success" class="success" data-testid="success-message">{{ success }}</p>

    <form data-testid="register-form" @submit.prevent="register">
      <div class="form-group">
        <label for="email">Email</label>
        <input id="email" name="email" type="email" v-model="email" />
      </div>

      <div class="form-group">
        <label for="password">Password</label>
        <input id="password" name="password" type="password" v-model="password" />
      </div>

      <div class="form-group">
        <label for="confirmPassword">Confirm Password</label>
        <input id="confirmPassword" name="confirmPassword" type="password" v-model="confirmPassword" />
      </div>

      <button type="submit">Create account</button>
    </form>

    <p>Already have an account? <NuxtLink to="/login">Login</NuxtLink></p>
  </main>
</template>
