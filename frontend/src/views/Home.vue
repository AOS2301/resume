<script setup>
import NavBar from '../components/NavBar.vue'
import '../assets/home.css'
</script>
<template>
  <main class="home">
    <NavBar />
    <section class="hero">
      <div class="hero-content">
        <span class="availability-badge">
          <span class="badge-dot"></span>
          DISPONÍVEL PARA NOVOS DESAFIOS
        </span>

        <div class="hero-name">
          <h1 class="name-first">Arthur Osvaldo</h1>
          <h1 class="name-last">Schmitz</h1>
        </div>

        <p class="hero-bio">
          Desenvolvedor full stack júnior focado em aplicações web modernas utilizando Vue.js, Node.js e JavaScript.
          Possuo experiência com integração de APIs, requisições HTTP e bancos de dados PostgreSQL.
          Gosto de aprender novas tecnologias e estou constantemente buscando evoluir minhas habilidades no desenvolvimento de software.
        </p>
      </div>
    </section>
  </main>
</template>