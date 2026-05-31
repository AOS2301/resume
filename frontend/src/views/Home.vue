<script setup>
import '../assets/home.css'
import NavBar from '../components/NavBar.vue'
</script>

<template>
  <main class="home">
    <NavBar />

    <!-- ── HERO ──────────────────────────────────────── -->
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
          Gosto de aprender novas tecnologias e estou constantemente buscando evoluir minhas habilidades no
          desenvolvimento de software.
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
          <img src="../data/img/home/aos.png" alt="Arthur Osvaldo Schmitz" class="hero-photo" />
        </div>
        <div class="social-links">
          <a href="https://www.linkedin.com/in/arthurschmitz/" target="_blank" class="social-link"
            aria-label="LinkedIn">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round"
              stroke-linejoin="round">
              <rect x="2" y="2" width="20" height="20" rx="4" />
              <path d="M7 10v7M7 7v.01M12 17v-4a2 2 0 0 1 4 0v4M12 10v7" />
            </svg>
            LinkedIn
          </a>
          <a href="https://github.com/AOS2301" target="_blank" class="social-link" aria-label="GitHub">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round"
              stroke-linejoin="round">
              <path
                d="M9 19c-4.3 1.4-4.3-2.5-6-3m12 5v-3.5c0-1 .1-1.4-.5-2 2.8-.3 5.5-1.4 5.5-6a4.6 4.6 0 0 0-1.3-3.2 4.2 4.2 0 0 0-.1-3.2s-1.1-.3-3.5 1.3a12.3 12.3 0 0 0-6.2 0C6.5 2.8 5.4 3.1 5.4 3.1a4.2 4.2 0 0 0-.1 3.2A4.6 4.6 0 0 0 4 9.5c0 4.6 2.7 5.7 5.5 6-.6.6-.6 1.2-.5 2V21" />
            </svg>
            GitHub
          </a>
          <a href="https://www.instagram.com/arthur_schmitz06/" target="_blank" class="social-link"
            aria-label="Instagram">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round"
              stroke-linejoin="round">
              <rect x="2" y="2" width="20" height="20" rx="6" />
              <circle cx="12" cy="12" r="4" />
              <circle cx="17.5" cy="6.5" r=".5" fill="currentColor" />
            </svg>
            Instagram
          </a>
        </div>
      </div>
    </section>

    <!-- ── HABILIDADES ────────────────────────────────── -->
    <section class="section" id="habilidades">
      <div class="section-header">
        <span class="section-tag">// SKILLS</span>
        <h2 class="section-title">Habilidades Técnicas</h2>
      </div>

      <div class="skills-grid">
        <div class="skill-group" v-for="group in skillGroups" :key="group.category">
          <span class="skill-group-label">{{ group.category }}</span>
          <div class="skill-list">
            <div class="skill-item" v-for="skill in group.skills" :key="skill.name">
              <div class="skill-info">
                <span class="skill-name">{{ skill.name }}</span>
                <span class="skill-level">{{ skill.level }}</span>
              </div>
              <div class="skill-bar">
                <div class="skill-fill" :style="{ width: skill.percent + '%' }"></div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- ── FORMAÇÃO ACADÊMICA ─────────────────────────── -->
    <section class="section" id="formacao">
      <div class="section-header">
        <span class="section-tag">// FORMAÇÃO</span>
        <h2 class="section-title">Carreira Acadêmica</h2>
      </div>

      <div class="timeline">
        <div class="timeline-item" v-for="edu in education" :key="edu.institution">
          <div class="timeline-dot"></div>
          <div class="timeline-card">
            <div class="timeline-top">
              <div>
                <h3 class="timeline-title">{{ edu.degree }}</h3>
                <span class="timeline-institution">{{ edu.institution }}</span>
              </div>
              <span class="timeline-period">{{ edu.period }}</span>
            </div>
            <p class="timeline-desc">{{ edu.description }}</p>
            <div class="timeline-tags" v-if="edu.highlights && edu.highlights.length">
              <span class="timeline-tag" v-for="h in edu.highlights" :key="h">{{ h }}</span>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- ── CURSOS & CERTIFICADOS ──────────────────────── -->
    <section class="section" id="cursos">
      <div class="section-header">
        <span class="section-tag">// QUALIFICAÇÕES</span>
        <h2 class="section-title">Cursos & Certificados</h2>
      </div>

      <div class="certs-grid">
        <article class="cert-card" v-for="cert in certifications" :key="cert.title">
          <div class="cert-top">
            <span class="cert-category" :class="'cert-category--' + cert.category">
              {{ cert.categoryLabel }}
            </span>
            <span class="cert-year">{{ cert.year }}</span>
          </div>
          <h3 class="cert-title">{{ cert.title }}</h3>
          <span class="cert-issuer">{{ cert.issuer }}</span>
          <div class="cert-footer">
            <div class="cert-skills">
              <span class="cert-skill" v-for="s in cert.skills" :key="s">{{ s }}</span>
            </div>
            <a v-if="cert.credentialUrl" :href="cert.credentialUrl" target="_blank" class="cert-link"
              aria-label="Ver credencial">
              <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round"
                stroke-linejoin="round">
                <path d="M18 13v6a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h6" />
                <polyline points="15 3 21 3 21 9" />
                <line x1="10" y1="14" x2="21" y2="3" />
              </svg>
            </a>
          </div>
        </article>
      </div>
    </section>

    <!-- ── EXPERIÊNCIA PROFISSIONAL ───────────────────── -->
    <section class="section" id="experiencia">
      <div class="section-header">
        <span class="section-tag">// EXPERIÊNCIA</span>
        <h2 class="section-title">Trajetória Profissional</h2>
      </div>

      <div class="timeline">
        <div class="timeline-item" v-for="job in experience" :key="job.company + job.period">
          <div class="timeline-dot timeline-dot--accent"></div>
          <div class="timeline-card">
            <div class="timeline-top">
              <div>
                <h3 class="timeline-title">{{ job.role }}</h3>
                <span class="timeline-institution">{{ job.company }}</span>
              </div>
              <span class="timeline-period">{{ job.period }}</span>
            </div>
            <p class="timeline-desc">{{ job.description }}</p>
            <div class="timeline-tags" v-if="job.techs && job.techs.length">
              <span class="timeline-tag" v-for="t in job.techs" :key="t">{{ t }}</span>
            </div>
          </div>
        </div>
      </div>
    </section>


  </main>
</template>

<script>
export default {
  data() {
    return {
      techStack: [
        { name: 'Vue.js', color: '#42b883' },
        { name: 'JavaScript', color: '#f7df1e' },
        { name: 'HTML5', color: '#e34c26' },
        { name: 'CSS3', color: '#264de4' },
        { name: 'Node.js', color: '#68a063' },
        { name: 'Express.js', color: '#000000' },
        { name: 'REST APIs', color: '#5b5ef4' },
        { name: 'PostgreSQL', color: '#336791' },
        { name: 'Git', color: '#f05032' },
        { name: 'Docker', color: '#2496ed' },
        { name: 'Linux', color: '#333333' },
        { name: 'Java (basics)', color: '#b07219' }
      ],

      education: [
        {
          degree: 'Bacharelado em Ciência da Computação',
          institution: 'UNISINOS',
          period: '2026 – Atualmente',
          description: 'Curso focado no desenvolvimento de software, estruturas de dados, banco de dados relacionais, engenharia de software e desenvolvimento web. Substitua com sua instituição real.',
          highlights: ['POO', 'Banco de Dados', 'Eng. de Software', 'Redes'],
        },
        {
          degree: 'Bacharelado em Ciência da Computação',
          institution: 'Feevale',
          period: '2024 – 2025',
          description: 'Curso focado no desenvolvimento de software, estruturas de dados, banco de dados relacionais, engenharia de software e desenvolvimento web. Substitua com sua instituição real.',
          highlights: ['POO', 'Banco de Dados', 'Eng. de Software', 'Redes'],
        },
        {
          degree: 'Técnico em Informática',
          institution: 'Instituto Ivoti',
          period: '2021 – 2023',
          description: 'Formação técnica com ênfase em programação, lógica de computação e infraestrutura de TI. Adicione detalhes reais da sua formação técnica.',
          highlights: ['Lógica de Programação', 'Redes', 'Hardware'],
        },
      ],

      certifications: [
        {
          title: 'Vue.js 3 — Completo',
          issuer: 'Udemy',
          year: '2024',
          category: 'frontend',
          categoryLabel: 'Frontend',
          skills: ['Vue 3', 'Composition API', 'Vuex', 'Router'],
          credentialUrl: null,
        },
        {
          title: 'Node.js: API RESTful com Express',
          issuer: 'Udemy',
          year: '2024',
          category: 'backend',
          categoryLabel: 'Backend',
          skills: ['Node.js', 'Express', 'JWT', 'PostgreSQL'],
          credentialUrl: null,
        },
        {
          title: 'JavaScript Moderno — ES6+',
          issuer: 'Origamid / Udemy',
          year: '2023',
          category: 'linguagem',
          categoryLabel: 'Linguagem',
          skills: ['ES6+', 'Async/Await', 'Modules', 'DOM'],
          credentialUrl: null,
        },
        {
          title: 'Git & GitHub — Do Iniciante ao Avançado',
          issuer: 'Udemy',
          year: '2023',
          category: 'devops',
          categoryLabel: 'DevOps',
          skills: ['Git', 'Branching', 'Pull Request', 'CI'],
          credentialUrl: null,
        },
        {
          title: 'SQL e PostgreSQL — Completo',
          issuer: 'Udemy',
          year: '2023',
          category: 'banco',
          categoryLabel: 'Banco de Dados',
          skills: ['PostgreSQL', 'Joins', 'Índices', 'Views'],
          credentialUrl: null,
        },
        {
          title: 'HTML & CSS — Responsivo e Moderno',
          issuer: 'Origamid',
          year: '2022',
          category: 'frontend',
          categoryLabel: 'Frontend',
          skills: ['CSS Grid', 'Flexbox', 'Responsivo', 'BEM'],
          credentialUrl: null,
        },
      ],

      experience: [
        {
          role: 'Desenvolvedor Full Stack Júnior',
          company: 'PRD Tecnologia e gestão',
          period: 'Jun 2026 – Atualmente',
          description: 'Desenvolvimento e manutenção de aplicações web utilizando Vue.js no frontend e Node.js no backend. Integração com APIs externas e modelagem de banco de dados PostgreSQL. Substitua com sua experiência real.',
          techs: ['Vue.js', 'Node.js', 'PostgreSQL', 'REST API'],
        },
        {
          role: 'Desenvolvedor Java Júnior',
          company: 'PRD Tecnologia e gestão',
          period: 'fev 2024 – set 2025',
          description: 'Desenvolvimento e manutenção de aplicações web utilizando Vue.js no frontend e Node.js no backend. Integração com APIs externas e modelagem de banco de dados PostgreSQL. Substitua com sua experiência real.',
          techs: ['Vue.js', 'Node.js', 'PostgreSQL', 'REST API'],
        },
        {
          role: 'Estágio Desenvolvedor ERP',
          company: 'PRD Tecnologia e gestão',
          period: 'Ago 2023 – fev 2024',
          description: 'Auxílio no desenvolvimento de interfaces responsivas e consumo de APIs REST. Participação em reuniões de equipe e code reviews. Substitua com sua experiência real.',
          techs: ['JavaScript', 'HTML/CSS', 'Vue.js', 'Git'],
        },
      ],

      skillGroups: [
        {
          category: 'Frontend',
          skills: [
            { name: 'Vue.js', level: 'Intermediário', percent: 75 },
            { name: 'JavaScript', level: 'Intermediário', percent: 72 },
            { name: 'HTML / CSS', level: 'Avançado', percent: 85 },
          ],
        },
        {
          category: 'Backend',
          skills: [
            { name: 'Node.js', level: 'Intermediário', percent: 75 },
            { name: 'Java', level: 'Básico', percent: 45 },
            { name: 'Express.js', level: 'Intermediário', percent: 72 },
            { name: 'REST APIs', level: 'Intermediário', percent: 75 },
            { name: 'PostgreSQL', level: 'Intermediário', percent: 80 },
          ],
        },
        {
          category: 'Ferramentas',
          skills: [
            { name: 'Git / GitHub', level: 'Avançado', percent: 85 },
            { name: 'Docker', level: 'Básico', percent: 55 },
            { name: 'Linux', level: 'Básico', percent: 35 },
          ],
        },
      ]
    }
  }
}
</script>