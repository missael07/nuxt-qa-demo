<script setup lang="ts">
const email = ref('')

onMounted(() => {
  const isLoggedIn = localStorage.getItem('qa_logged_in') === 'true'
  if (!isLoggedIn) {
    navigateTo('/login')
    return
  }
  email.value = localStorage.getItem('qa_user_email') || ''
})

function logout() {
  localStorage.removeItem('qa_logged_in')
  navigateTo('/login')
}
</script>

<template>
  <main class="card">
    <h1>Dashboard</h1>
    <p data-testid="welcome-message">Welcome {{ email }}</p>
    <button type="button" @click="logout">Logout</button>
  </main>
</template>
