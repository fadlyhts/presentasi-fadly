<script setup>
import { ref, onMounted } from 'vue'
import { ArrowDown, Sparkles } from 'lucide-vue-next'
import GridDistortion from './GridDistortion.vue'
import backgroundImage from '@/assets/background.png'

const isVisible = ref(false)

const scrollToProfile = () => {
  const element = document.querySelector('#profil')
  if (element) {
    element.scrollIntoView({ behavior: 'smooth' })
  }
}

onMounted(() => {
  // Trigger animation after component mounts
  setTimeout(() => {
    isVisible.value = true
  }, 100)
})
</script>

<template>
  <section id="home" class="hero-section">
    <!-- Vue Bits GridDistortion Background -->
    <div class="hero-background">
      <GridDistortion
        :imageSrc="backgroundImage"
        :grid="12"
        :mouse="0.15"
        :strength="0.2"
        :relaxation="0.9"
        className="grid-bg"
      />
      <div class="hero-overlay"></div>
    </div>

    <div class="hero-content" :class="{ 'visible': isVisible }">
      <!-- Decorative Elements -->
      <div class="hero-badge">
        <Sparkles :size="16" class="text-emerald-400" />
        <span>Presentasi Magenta Batch 2 - 2025</span>
      </div>

      <!-- Main Title -->
      <h1 class="hero-title">
        <span class="hero-title-line">Project</span>
        <span class="hero-title-line gradient-text">Charter</span>
      </h1>

      <!-- Presenter Name -->
      <div class="hero-presenter">
        <span class="hero-presenter-label">Presented by</span>
        <h2 class="hero-presenter-name">Ahmad Fadli Hutasuhut</h2>
      </div>

      <!-- Tech Stack -->
      <div class="hero-tech">
        <span class="tech-badge">Vue.js</span>
        <span class="tech-badge">Vue Bits</span>
        <span class="tech-badge">Shadcn Vue</span>
        <span class="tech-badge">Three.js</span>
      </div>

      <!-- Scroll Indicator -->
      <button class="scroll-indicator" @click="scrollToProfile">
        <span>Explore</span>
        <ArrowDown :size="20" class="scroll-arrow" />
      </button>
    </div>
  </section>
</template>

<style scoped>
.hero-section {
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  overflow: hidden;
  padding: 120px 24px 80px;
}

.hero-background {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 0;
}

.hero-background :deep(.grid-bg) {
  width: 100%;
  height: 100%;
}

.hero-overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(
    to bottom,
    rgba(255, 255, 255, 0.3) 0%,
    rgba(255, 255, 255, 0.1) 50%,
    rgba(255, 255, 255, 0.7) 100%
  );
  pointer-events: none;
}

.hero-content {
  text-align: center;
  z-index: 10;
  opacity: 0;
  transform: translateY(40px);
  transition: all 0.8s cubic-bezier(0.16, 1, 0.3, 1);
  position: relative;
}

.hero-content.visible {
  opacity: 1;
  transform: translateY(0);
}

.hero-badge {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  background: rgba(16, 185, 129, 0.1);
  border: 1px solid rgba(16, 185, 129, 0.3);
  padding: 8px 20px;
  border-radius: 9999px;
  font-size: 0.875rem;
  font-weight: 500;
  color: var(--color-primary-light);
  margin-bottom: 32px;
  animation: pulse-glow 3s ease-in-out infinite;
  backdrop-filter: blur(10px);
}

.hero-title {
  font-size: clamp(2.5rem, 8vw, 5rem);
  font-weight: 800;
  line-height: 1.1;
  margin-bottom: 24px;
  letter-spacing: -0.03em;
}

.hero-title-line {
  display: block;
}

.hero-presenter {
  margin-bottom: 40px;
}

.hero-presenter-label {
  display: block;
  font-size: 0.9rem;
  color: var(--color-text-secondary);
  text-transform: uppercase;
  letter-spacing: 0.2em;
  margin-bottom: 8px;
}

.hero-presenter-name {
  font-size: clamp(1.5rem, 4vw, 2.5rem);
  font-weight: 700;
  color: var(--color-text-primary);
}

.hero-tech {
  display: flex;
  flex-wrap: wrap;
  gap: 12px;
  justify-content: center;
  margin-bottom: 60px;
}

.tech-badge {
  background: rgba(148, 163, 184, 0.1);
  border: 1px solid rgba(148, 163, 184, 0.2);
  padding: 8px 16px;
  border-radius: 8px;
  font-size: 0.85rem;
  font-weight: 500;
  color: var(--color-text-secondary);
  transition: all 0.3s ease;
  backdrop-filter: blur(10px);
}

.tech-badge:hover {
  background: rgba(16, 185, 129, 0.1);
  border-color: rgba(16, 185, 129, 0.3);
  color: var(--color-primary-light);
}

.scroll-indicator {
  display: inline-flex;
  flex-direction: column;
  align-items: center;
  gap: 8px;
  background: none;
  border: none;
  color: var(--color-text-secondary);
  cursor: pointer;
  font-size: 0.875rem;
  font-weight: 500;
  transition: color 0.3s ease;
}

.scroll-indicator:hover {
  color: var(--color-primary-light);
}

.scroll-arrow {
  animation: bounce 2s ease-in-out infinite;
}

@keyframes bounce {
  0%, 100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(8px);
  }
}

@media (max-width: 768px) {
  .hero-section {
    padding: 100px 16px 60px;
  }
  
  .hero-tech {
    gap: 8px;
  }
  
  .tech-badge {
    padding: 6px 12px;
    font-size: 0.75rem;
  }
}
</style>

