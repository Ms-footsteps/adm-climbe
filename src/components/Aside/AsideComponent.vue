<template>
  <aside class="sidebar" v-if="!route.meta.noSidebar">
    <img src="/img/climbe-logo.png" alt="logo Climbe" class="logo" />

    <div class="profile">
      <p class="profile-name">{{ userName }}</p>
      <p class="profile-email">{{ userEmail }}</p>
    </div>

    <nav class="menu-btn-content">
      <MenuButton text="Usuários" link="/users" />
    </nav>
  </aside>
</template>

<script setup>
import { useRoute }     from 'vue-router'
import { ref, onMounted } from 'vue'
import {jwtDecode}       from 'jwt-decode'
import MenuButton       from './components/MenuButton.vue'
const route = useRoute()
const userName  = ref('')
const userEmail = ref('')

onMounted(() => {
  const token = localStorage.getItem('token')
  if (!token) return

  try {
    const payload = jwtDecode(token)
    userName.value  = payload.name  || ''
    userEmail.value = payload.email || ''
  } catch (err) {
    console.error(err)
  }
})
</script>

<style scoped>
.sidebar {
  grid-area: sidebar;
  background: rgba(0, 0, 0, 0.7);
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 1.5rem 1rem;
  box-shadow: 1px 0 9px rgba(0, 0, 0, 0.75);
}

.logo {
  width: 12rem;
  margin-bottom: 1.5rem;
}

.profile {
  text-align: center;
  margin-bottom: 2rem;
}

.profile-name {
  color: #fff;
  font-weight: bold;
  margin: 0;
}

.profile-email {
  color: #ccc;
  font-size: 0.9rem;
  margin: 0;
}

.menu-btn-content {
  width: 100%;
  display: flex;
  flex-direction: column;
  gap: 1rem;
}
</style>
