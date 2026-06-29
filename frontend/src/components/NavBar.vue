<script setup>
import { ref } from 'vue'
import { RouterLink, useRouter } from 'vue-router'
import '../assets/nav-bar.css'

const isOpen = ref(false)
const router = useRouter()

function toggleMenu() {
  isOpen.value = !isOpen.value
  document.body.style.overflow = isOpen.value ? 'hidden' : ''
}

function closeMenu() {
  isOpen.value = false
  document.body.style.overflow = ''
}

router.afterEach(() => closeMenu())
</script>

<template>
  <header class="navbar">
    <div class="navbar-logo">
      <RouterLink to="/" class="logo-link">AOS.DEV</RouterLink>
    </div>

    <nav class="navbar-nav" :class="{ 'is-open': isOpen }">
      <RouterLink to="/" class="nav-link" @click="closeMenu">SUMMARY</RouterLink>
      <RouterLink to="/projects" class="nav-link" @click="closeMenu">PROJECTS</RouterLink>
    </nav>

    <button
      class="nav-toggle"
      :class="{ 'is-open': isOpen }"
      :aria-label="isOpen ? 'Fechar menu' : 'Abrir menu'"
      :aria-expanded="isOpen"
      @click="toggleMenu"
    >
      <span></span>
      <span></span>
      <span></span>
    </button>
  </header>
</template>