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
          Desenvolvedor de software com experiência em aplicações web utilizando Java, Vue.js, JavaScript e PostgreSQL.
          Atuo no desenvolvimento e manutenção de sistemas empresariais, integrações de APIs e modelagem de banco de
          dados.
          Atualmente curso Ciência da Computação e busco evoluir continuamente minhas habilidades em desenvolvimento de
          software e arquitetura de sistemas.
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
        { name: 'Java', color: '#b07219' },
        { name: 'JavaScript', color: '#f7df1e' },
        { name: 'PostgreSQL', color: '#336791' },
        { name: 'Node.js', color: '#68a063' },
        { name: 'REST APIs', color: '#5b5ef4' },
        { name: 'Git', color: '#f05032' },
        { name: 'Linux', color: '#333333' }
      ],

      education: [
        {
          degree: 'Bacharelado em Ciência da Computação',
          institution: 'UNISINOS',
          period: '2026 – Atualmente',
          description: 'Graduação voltada para desenvolvimento de software, algoritmos, estruturas de dados, banco de dados, engenharia de software e arquitetura de sistemas.',
          highlights: [
            'POO',
            'Estruturas de Dados',
            'Banco de Dados',
            'Engenharia de Software'
          ],
        },
        {
          degree: 'Intercâmbio de Inglês',
          institution: 'Melbourne, Austrália',
          period: 'Set 2025 – Jan 2026',
          description: 'Experiência internacional voltada ao aprimoramento do idioma inglês e desenvolvimento pessoal em ambiente multicultural.',
          highlights: [
            'Inglês',
            'Comunicação',
            'Experiência Internacional'
          ],
        },
        {
          degree: 'Bacharelado em Ciência da Computação',
          institution: 'Feevale',
          period: '2024 – 2025',
          description: 'Formação acadêmica focada em fundamentos da computação, programação, banco de dados e desenvolvimento de software.',
          highlights: [
            'Algoritmos',
            'POO',
            'Banco de Dados',
            'Desenvolvimento Web'
          ],
        },
        {
          degree: 'Técnico em Informática',
          institution: 'Instituto Ivoti',
          period: '2021 – 2023',
          description: 'Formação técnica de três anos com foco em lógica de programação, desenvolvimento de software, banco de dados, redes de computadores e fundamentos de tecnologia da informação.',
          highlights: [
            'Lógica de Programação',
            'Banco de Dados',
            'Redes',
            'Desenvolvimento'
          ],
        },
      ],

      certifications: [
        {
          title: 'O Curso Definitivo de Lógica de Programação',
          issuer: 'Udemy',
          year: '2024',
          category: 'linguagem',
          categoryLabel: 'Programação',
          skills: [
            'VisualG',
            'C',
            'C++',
            'Python',
            'Java'
          ],
          credentialUrl: null,
        },
        {
          title: 'Dominando Banco de Dados, Conceitos e Linguagem SQL',
          issuer: 'Udemy',
          year: '2024',
          category: 'banco',
          categoryLabel: 'Banco de Dados',
          skills: [
            'SQL',
            'Modelagem',
            'SQL Server',
            'Administração de Banco'
          ],
          credentialUrl: null,
        },
      ],

      experience: [
        {
          role: 'Desenvolvedor Full Stack Júnior',
          company: 'PRD Tecnologia e Gestão',
          period: 'Jan 2026 – Atualmente',
          description: 'Atuação no desenvolvimento e manutenção de sistemas empresariais utilizando Java, Vue.js e PostgreSQL. Responsável pela implementação de novas funcionalidades, correção de problemas em ambiente produtivo, desenvolvimento de interfaces web, integração entre sistemas via APIs REST e criação de consultas SQL para suporte às regras de negócio. Participação na manutenção de relatórios JasperReports e soluções de impressão térmica utilizadas por clientes.',
          techs: [
            'Java',
            'Vue.js',
            'PostgreSQL',
            'REST APIs',
            'JasperReports',
            'Git'
          ],
        },

        {
          role: 'Desenvolvedor Java Júnior',
          company: 'PRD Tecnologia e Gestão',
          period: 'Fev 2024 – Jun 2025',
          description: 'Desenvolvimento e manutenção de funcionalidades em sistemas ERP corporativos utilizando Java e PostgreSQL. Atuação na análise e correção de defeitos, criação de consultas SQL, manutenção de relatórios gerenciais, implementação de regras de negócio e suporte técnico para demandas internas e de clientes.',
          techs: [
            'Java',
            'PostgreSQL',
            'SQL',
            'JasperReports',
            'SVN'
          ],
        },

        {
          role: 'Estagiário de Desenvolvimento ERP',
          company: 'PRD Tecnologia e Gestão',
          period: 'Ago 2023 – Fev 2024',
          description: 'Participação no desenvolvimento e suporte de sistemas ERP, realizando manutenção de funcionalidades existentes, testes, consultas em banco de dados, análise de chamados e auxílio na resolução de problemas reportados por usuários. Contato direto com processos de negócio e práticas de desenvolvimento utilizadas em ambiente corporativo.',
          techs: [
            'Java',
            'PostgreSQL',
            'SQL',
            'SVN'
          ],
        },
      ],

      skillGroups: [
        {
          category: 'Frontend',
          skills: [
            { name: 'Vue.js', level: 'Intermediário', percent: 75 },
            { name: 'JavaScript', level: 'Intermediário', percent: 70 },
            { name: 'HTML / CSS', level: 'Intermediário+', percent: 80 },
          ],
        },
        {
          category: 'Backend',
          skills: [
            { name: 'Node.js', level: 'Intermediário', percent: 65 },
            { name: 'Express.js', level: 'Intermediário', percent: 70 },
            { name: 'REST APIs', level: 'Intermediário+', percent: 80 },
            { name: 'Java', level: 'Intermediário', percent: 65 },
          ],
        },
        {
          category: 'Banco de Dados',
          skills: [
            { name: 'PostgreSQL', level: 'Intermediário+', percent: 82 },
            { name: 'SQL', level: 'Intermediário+', percent: 80 },
          ],
        },
        {
          category: 'Ferramentas',
          skills: [
            { name: 'Git / GitHub', level: 'Básico', percent: 45 },
            { name: 'Docker', level: 'Básico', percent: 45 },
            { name: 'Linux', level: 'Iniciante', percent: 30 },
          ],
        },
      ],
    }
  }
}
</script>