<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import NavBar from '../components/NavBar.vue'
import '../assets/project.css'
import overrides from '../data/project-overrides.json'

// Importa todas as imagens da pasta de uma vez
const imageModules = import.meta.glob('../data/img/*', { eager: true })

function resolveImg(filename) {
  const key = `../data/img/${filename}`
  return imageModules[key]?.default ?? ''
}

// ── Configuração ─────────────────────────────────────────────────────────
const GITHUB_USERNAME = 'AOS2301'
const HIDE_FORKS = true
const FILTER_BY_TOPIC = false
const REQUIRED_TOPIC = 'portfolio'

const HIDDEN_REPOS = ['readme', GITHUB_USERNAME]

const PRIORITY_ORDER = ['shift', 'gymsystem', 'portfolio', 'portifolio']

function sortByPriority(list) {
  const rank = item => {
    const name = item.name.toLowerCase()
    const idx = PRIORITY_ORDER.findIndex(p => name.includes(p))
    return idx === -1 ? Infinity : idx
  }
  return [...list].sort((a, b) => rank(a) - rank(b))
}

const EXTRA_PROJECTS = [
  {
    name: 'Caça ao Tesouro — DACathon Feevas',
    summary: 'Sistema de caça ao tesouro desenvolvido para a gincana da minha antiga escola, com desafios, dicas e progressão de fases.',
    description: 'Projeto desenvolvido para uma gincana escolar onde atuei como organizador do evento e responsável pelos desafios digitais. Foi construído com HTML, CSS e JavaScript puro, focando em simplicidade e rapidez para funcionar durante o fim de semana da competição. O sistema possuía progressão de fases, validação de respostas e páginas interativas para cada desafio.',
    repo: 'https://github.com/orgs/DACathonFeevas/repositories',
    site: '',
    tags: ['SpringBoot', 'JavaScript', 'html', 'css'],
    images: ['DacFunctionality.png', 'caminhoCritico.png', 'loginDac.png']
  }
]
// ────────────────────────────────────────────────────────────────────────

const projects = ref([])
const loading = ref(true)
const loadError = ref(false)

async function loadProjects() {
  loading.value = true
  loadError.value = false
  try {
    const res = await fetch(
      `https://api.github.com/users/${GITHUB_USERNAME}/repos?per_page=100&sort=updated`
    )
    if (!res.ok) throw new Error(`GitHub API respondeu ${res.status}`)
    let repos = await res.json()

    if (HIDE_FORKS) repos = repos.filter(r => !r.fork)
    if (FILTER_BY_TOPIC) {
      repos = repos.filter(r => (r.topics || []).includes(REQUIRED_TOPIC))
    }
    repos = repos.filter(
      r => !HIDDEN_REPOS.some(hidden => hidden.toLowerCase() === r.name.toLowerCase())
    )

    const fromGithub = repos.map((repo, i) => {
      const override = overrides[repo.name] || {}

      const images = (override.images && override.images.length
        ? override.images
        : ['placeholder.png']
      ).map(resolveImg)

      return {
        id: i,
        name: override.name || repo.name,
        summary: override.summary || 'Sem descrição.',
        description: override.description || 'Sem descrição detalhada.',
        repo: repo.html_url,
        site: override.site || repo.homepage || '',
        tags: override.tags && override.tags.length
          ? override.tags
          : (repo.topics && repo.topics.length ? repo.topics : [repo.language].filter(Boolean)),
        images
      }
    })

    const manual = EXTRA_PROJECTS.map((p, i) => ({
      id: `extra-${i}`,
      ...p,
      images: (p.images.length ? p.images : ['placeholder.png']).map(resolveImg)
    }))

    projects.value = sortByPriority([...fromGithub, ...manual])
  } catch (err) {
    console.error('Erro ao buscar repositórios do GitHub:', err)
    loadError.value = true
  } finally {
    loading.value = false
  }
}

const cardImageIndex = ref({})

function currentCardImage(project) {
  const idx = cardImageIndex.value[project.id] || 0
  return project.images[idx] ?? project.images[0]
}

function cardPrevImage(e, project) {
  e.stopPropagation()
  if (project.images.length < 2) return
  const len = project.images.length
  const cur = cardImageIndex.value[project.id] || 0
  cardImageIndex.value[project.id] = (cur - 1 + len) % len
}

function cardNextImage(e, project) {
  e.stopPropagation()
  if (project.images.length < 2) return
  const len = project.images.length
  const cur = cardImageIndex.value[project.id] || 0
  cardImageIndex.value[project.id] = (cur + 1) % len
}

// Ao sair do card com o mouse, volta pra primeira imagem
function resetCardImage(project) {
  cardImageIndex.value[project.id] = 0
}

// ── Modal state ────────────────────────────────────────────────────────────
const activeProject = ref(null)
const slideIndex = ref(0)

function openProject(p) {
  activeProject.value = p
  slideIndex.value = 0
  document.body.style.overflow = 'hidden'
}

function closeModal() {
  activeProject.value = null
  document.body.style.overflow = ''
}

function prevSlide() {
  const len = activeProject.value.images.length
  slideIndex.value = (slideIndex.value - 1 + len) % len
}

function nextSlide() {
  const len = activeProject.value.images.length
  slideIndex.value = (slideIndex.value + 1) % len
}

function onKeydown(e) {
  if (!activeProject.value) return
  if (e.key === 'Escape') closeModal()
  if (e.key === 'ArrowLeft') prevSlide()
  if (e.key === 'ArrowRight') nextSlide()
}

onMounted(() => {
  window.addEventListener('keydown', onKeydown)
  loadProjects()
})
onUnmounted(() => window.removeEventListener('keydown', onKeydown))

// ── Magnetic tilt on cards ─────────────────────────────────────────────────
function onCardMouseMove(e, el) {
  const rect = el.getBoundingClientRect()
  const cx = rect.left + rect.width / 2
  const cy = rect.top + rect.height / 2
  const dx = (e.clientX - cx) / (rect.width / 2)
  const dy = (e.clientY - cy) / (rect.height / 2)
  el.style.transform = `perspective(800px) rotateY(${dx * 8}deg) rotateX(${-dy * 8}deg) translateZ(10px)`
}

function onCardMouseLeave(el, project) {
  el.style.transform = 'perspective(800px) rotateY(0deg) rotateX(0deg) translateZ(0px)'
  if (project) resetCardImage(project)
}
</script>

<template>
  <main class="projects-page">
    <NavBar />

    <section class="projects-section">
      <div class="section-header">
        <h2 class="section-title">Projetos</h2>
      </div>

      <p v-if="loading" class="section-status">Carregando projetos do GitHub...</p>
      <p v-else-if="loadError" class="section-status">Não foi possível carregar os projetos agora.</p>

      <div v-else class="cards-grid">
        <div v-for="(project, i) in projects" :key="project.id" class="card" :style="{ animationDelay: `${i * 80}ms` }"
          @mousemove="onCardMouseMove($event, $event.currentTarget)"
          @mouseleave="onCardMouseLeave($event.currentTarget)" @click="openProject(project)">
          <div class="card-thumb">
            <img :src="project.images[0]" :alt="project.name" loading="lazy" />
            <div class="card-thumb-overlay" />
          </div>

          <div class="card-body">
            <h3 class="card-name">{{ project.name }}</h3>
            <p class="card-summary">{{ project.summary }}</p>

            <div class="card-tags">
              <span v-for="tag in project.tags.slice(0, 3)" :key="tag" class="tag">{{ tag }}</span>
            </div>

            <div class="card-links" @click.stop>
              <a :href="project.repo" target="_blank" rel="noopener" class="card-link">
                <svg width="14" height="14" viewBox="0 0 24 24" fill="currentColor">
                  <path
                    d="M12 0C5.37 0 0 5.37 0 12c0 5.31 3.435 9.795 8.205 11.385.6.105.825-.255.825-.57 0-.285-.015-1.23-.015-2.235-3.015.555-3.795-.735-4.035-1.41-.135-.345-.72-1.41-1.23-1.695-.42-.225-1.02-.78-.015-.795.945-.015 1.62.87 1.845 1.23 1.08 1.815 2.805 1.305 3.495.99.105-.78.42-1.305.765-1.605-2.67-.3-5.46-1.335-5.46-5.925 0-1.305.465-2.385 1.23-3.225-.12-.3-.54-1.53.12-3.18 0 0 1.005-.315 3.3 1.23.96-.27 1.98-.405 3-.405s2.04.135 3 .405c2.295-1.56 3.3-1.23 3.3-1.23.66 1.65.24 2.88.12 3.18.765.84 1.23 1.905 1.23 3.225 0 4.605-2.805 5.625-5.475 5.925.435.375.81 1.095.81 2.22 0 1.605-.015 2.895-.015 3.3 0 .315.225.69.825.57A12.02 12.02 0 0 0 24 12c0-6.63-5.37-12-12-12z" />
                </svg>
                Repo
              </a>
              <a v-if="project.site" :href="project.site" target="_blank" rel="noopener"
                class="card-link card-link--site">
                <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <path d="M18 13v6a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h6" />
                  <polyline points="15 3 21 3 21 9" />
                  <line x1="10" y1="14" x2="21" y2="3" />
                </svg>
                Live
              </a>
            </div>
          </div>

          <div class="card-corner-arrow">↗</div>
        </div>
      </div>
    </section>

    <!-- ── Modal ──────────────────────────────────────────────────────────── -->
    <Transition name="modal">
      <div v-if="activeProject" class="modal-backdrop" @click.self="closeModal">
        <div class="modal">
          <button class="modal-close" @click="closeModal">✕</button>

          <div class="slideshow">
            <img :key="slideIndex" :src="activeProject.images[slideIndex]"
              :alt="`${activeProject.name} screenshot ${slideIndex + 1}`" class="slide-img" />

            <div v-if="activeProject.images.length > 1" class="slide-nav-zones">
              <button class="slide-zone slide-zone--prev" @click.stop="prevSlide" aria-label="Imagem anterior"></button>
              <button class="slide-zone slide-zone--next" @click.stop="nextSlide" aria-label="Próxima imagem"></button>
            </div>

            <div v-if="activeProject.images.length > 1" class="slide-controls">
              <button class="slide-btn" @click="prevSlide">‹</button>
              <div class="slide-dots">
                <span v-for="(_, idx) in activeProject.images" :key="idx" class="dot"
                  :class="{ active: idx === slideIndex }" @click="slideIndex = idx" />
              </div>
              <button class="slide-btn" @click="nextSlide">›</button>
            </div>
          </div>

          <div class="modal-info">
            <div class="modal-info-top">
              <h2 class="modal-title">{{ activeProject.name }}</h2>
              <div class="modal-tags">
                <span v-for="tag in activeProject.tags" :key="tag" class="tag tag--modal">{{ tag }}</span>
              </div>
            </div>

            <p class="modal-description">{{ activeProject.description }}</p>

            <div class="modal-links">
              <a :href="activeProject.repo" target="_blank" rel="noopener" class="modal-link">
                <svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor">
                  <path
                    d="M12 0C5.37 0 0 5.37 0 12c0 5.31 3.435 9.795 8.205 11.385.6.105.825-.255.825-.57 0-.285-.015-1.23-.015-2.235-3.015.555-3.795-.735-4.035-1.41-.135-.345-.72-1.41-1.23-1.695-.42-.225-1.02-.78-.015-.795.945-.015 1.62.87 1.845 1.23 1.08 1.815 2.805 1.305 3.495.99.105-.78.42-1.305.765-1.605-2.67-.3-5.46-1.335-5.46-5.925 0-1.305.465-2.385 1.23-3.225-.12-.3-.54-1.53.12-3.18 0 0 1.005-.315 3.3 1.23.96-.27 1.98-.405 3-.405s2.04.135 3 .405c2.295-1.56 3.3-1.23 3.3-1.23.66 1.65.24 2.88.12 3.18.765.84 1.23 1.905 1.23 3.225 0 4.605-2.805 5.625-5.475 5.925.435.375.81 1.095.81 2.22 0 1.605-.015 2.895-.015 3.3 0 .315.225.69.825.57A12.02 12.02 0 0 0 24 12c0-6.63-5.37-12-12-12z" />
                </svg>
                Ver Repositório
              </a>
              <a v-if="activeProject.site" :href="activeProject.site" target="_blank" rel="noopener"
                class="modal-link modal-link--primary">
                <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <path d="M18 13v6a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h6" />
                  <polyline points="15 3 21 3 21 9" />
                  <line x1="10" y1="14" x2="21" y2="3" />
                </svg>
                Acessar Site
              </a>
            </div>
          </div>
        </div>
      </div>
    </Transition>
  </main>
</template>