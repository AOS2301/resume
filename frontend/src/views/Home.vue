<script setup>
import '../assets/home.css'
import NavBar from '../components/NavBar.vue'
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

        <div class="tech-stack">
          <span class="tech-label">TECH STACK</span>
          <div class="tech-grid">
            <span class="tech-pill" v-for="tech in techStack" :key="tech.name">
              <span class="tech-dot" :style="{ background: tech.color }"></span>
              {{ tech.name }}
            </span>
          </div>
        </div>
      </div>

      <div class="hero-image-wrapper">
        <div class="hero-image">
        <img
          src="../data/img/home/aos.png"
          alt="Arthur Osvaldo Schmitz"
          class="hero-photo"
        />
      </div>
      <div class="social-links">
          <a 
            href="https://www.linkedin.com/in/arthurschmitz/" 
            target="_blank"
            class="social-link" 
            aria-label="LinkedIn"
          >
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round">
              <rect x="2" y="2" width="20" height="20" rx="4"/>
              <path d="M7 10v7M7 7v.01M12 17v-4a2 2 0 0 1 4 0v4M12 10v7"/>
            </svg>
            LinkedIn
          </a>
          <a 
            href="https://github.com/AOS2301" 
            target="_blank" 
            class="social-link" 
            aria-label="GitHub"
          >
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round">
              <path d="M9 19c-4.3 1.4-4.3-2.5-6-3m12 5v-3.5c0-1 .1-1.4-.5-2 2.8-.3 5.5-1.4 5.5-6a4.6 4.6 0 0 0-1.3-3.2 4.2 4.2 0 0 0-.1-3.2s-1.1-.3-3.5 1.3a12.3 12.3 0 0 0-6.2 0C6.5 2.8 5.4 3.1 5.4 3.1a4.2 4.2 0 0 0-.1 3.2A4.6 4.6 0 0 0 4 9.5c0 4.6 2.7 5.7 5.5 6-.6.6-.6 1.2-.5 2V21"/>
            </svg>
            GitHub
          </a>
          <a 
            href="https://www.instagram.com/arthur_schmitz06/" 
            target="_blank" 
            class="social-link" 
            aria-label="Instagram"
          >
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round">
              <rect x="2" y="2" width="20" height="20" rx="6"/>
              <circle cx="12" cy="12" r="4"/>
              <circle cx="17.5" cy="6.5" r=".5" fill="currentColor"/>
            </svg>
            Instagram
          </a>
        </div>
      </div>
    </section>

    <section class="projects" id="projetos">
      <div class="projects-header">
        <span class="section-tag">// PROJETOS</span>
        <h2 class="section-title">Em Destaque</h2>
      </div>

      <div class="projects-grid">
        <article class="project-card" v-for="project in projects" :key="project.title">
          <div class="project-card-top">
            <span class="project-tag">{{ project.tag }}</span>
            <div class="project-links">
              <a :href="project.github" target="_blank" class="project-icon-link" aria-label="Ver código">
                <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round">
                  <path d="M9 19c-4.3 1.4-4.3-2.5-6-3m12 5v-3.5c0-1 .1-1.4-.5-2 2.8-.3 5.5-1.4 5.5-6a4.6 4.6 0 0 0-1.3-3.2 4.2 4.2 0 0 0-.1-3.2s-1.1-.3-3.5 1.3a12.3 12.3 0 0 0-6.2 0C6.5 2.8 5.4 3.1 5.4 3.1a4.2 4.2 0 0 0-.1 3.2A4.6 4.6 0 0 0 4 9.5c0 4.6 2.7 5.7 5.5 6-.6.6-.6 1.2-.5 2V21"/>
                </svg>
              </a>
              <a v-if="project.live" :href="project.live" target="_blank" class="project-icon-link" aria-label="Ver ao vivo">
                <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round">
                  <path d="M18 13v6a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h6"/>
                  <polyline points="15 3 21 3 21 9"/>
                  <line x1="10" y1="14" x2="21" y2="3"/>
                </svg>
              </a>
            </div>
          </div>

          <h3 class="project-title">{{ project.title }}</h3>
          <p class="project-desc">{{ project.description }}</p>

          <div class="project-techs">
            <span class="project-tech" v-for="t in project.techs" :key="t">{{ t }}</span>
          </div>
        </article>
      </div>
    </section>

  </main>
</template>

<script>
export default {
  data() {
    return {
      techStack: [
        { name: 'Vue.js',      color: '#42b883' },
        { name: 'JavaScript',  color: '#f7df1e' },
        { name: 'Node.js',     color: '#68a063' },
        { name: 'PostgreSQL',  color: '#336791' },
        { name: 'HTML/CSS',    color: '#e34c26' },
        { name: 'REST APIs',   color: '#5b5ef4' },
        { name: 'Git',         color: '#f05032' },
        { name: 'TypeScript',  color: '#3178c6' },
      ],
      projects: [
        {
          title: 'Nome do Projeto 1',
          tag: 'Full Stack',
          description: 'Breve descrição do que o projeto faz, problema que resolve e tecnologias envolvidas. Substitua por seus projetos reais.',
          techs: ['Vue.js', 'Node.js', 'PostgreSQL'],
          github: 'https://github.com/AOS2301/projeto-1',
          live: 'https://projeto-1.vercel.app',
        },
        {
          title: 'Nome do Projeto 2',
          tag: 'Frontend',
          description: 'Breve descrição do que o projeto faz, problema que resolve e tecnologias envolvidas. Substitua por seus projetos reais.',
          techs: ['Vue.js', 'JavaScript', 'CSS'],
          github: 'https://github.com/AOS2301/projeto-2',
          live: null,
        },
        {
          title: 'Nome do Projeto 3',
          tag: 'Backend',
          description: 'Breve descrição do que o projeto faz, problema que resolve e tecnologias envolvidas. Substitua por seus projetos reais.',
          techs: ['Node.js', 'REST API', 'PostgreSQL'],
          github: 'https://github.com/AOS2301/projeto-3',
          live: null,
        },
      ]
    }
  }
}
</script>