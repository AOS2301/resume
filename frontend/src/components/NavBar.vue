<script setup>
import { RouterLink } from 'vue-router'
import '../assets/nav-bar.css'
</script>

<template>
  <header class="navbar">
    <div class="navbar-logo">
      <RouterLink to="/" class="logo-link">AOS.DEV</RouterLink>
    </div>
    <nav class="navbar-nav">
      <RouterLink to="/" class="nav-link">SUMMARY</RouterLink>
      <RouterLink to="/projects" class="nav-link">PROJECTS</RouterLink>
    </nav>
  </header>
</template>