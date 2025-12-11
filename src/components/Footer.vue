<script setup>
import { Heart, ExternalLink } from 'lucide-vue-next'

const techStack = [
  { name: 'Vue.js', url: 'https://vuejs.org' },
  { name: 'Vue Bits', url: 'https://vue-bits.dev' },
  { name: 'Shadcn Vue', url: 'https://shadcn-vue.com' },
  { name: 'Three.js', url: 'https://threejs.org' },
  { name: 'Tailwind CSS', url: 'https://tailwindcss.com' }
]
</script>

<template>
  <footer class="footer">
    <div class="container">
      <!-- Tech Stack -->
      <div class="footer-tech">
        <p class="footer-label">Built with</p>
        <div class="tech-links">
          <a 
            v-for="tech in techStack" 
            :key="tech.name"
            :href="tech.url"
            target="_blank"
            rel="noopener noreferrer"
            class="tech-link"
          >
            {{ tech.name }}
            <ExternalLink :size="12" class="link-icon" />
          </a>
        </div>
      </div>

      <div class="footer-divider"></div>

      <!-- Copyright -->
      <div class="footer-bottom">
        <p class="copyright">
          Made with <Heart :size="16" class="heart-icon" /> by Fadly
        </p>
        <p class="year">© {{ new Date().getFullYear() }} Presentasi Magang</p>
      </div>
    </div>
  </footer>
</template>

<style scoped>
.footer {
  padding: 60px 24px 40px;
  background: #f8fafc;
  border-top: 1px solid var(--color-border);
}

.footer-tech {
  text-align: center;
  margin-bottom: 32px;
}

.footer-label {
  font-size: 0.85rem;
  color: var(--color-text-secondary);
  margin-bottom: 16px;
  text-transform: uppercase;
  letter-spacing: 0.1em;
}

.tech-links {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 16px;
}

.tech-link {
  display: inline-flex;
  align-items: center;
  gap: 4px;
  padding: 8px 16px;
  background: rgba(148, 163, 184, 0.1);
  border: 1px solid var(--color-border);
  border-radius: 8px;
  color: var(--color-text-secondary);
  text-decoration: none;
  font-size: 0.85rem;
  font-weight: 500;
  transition: all 0.3s ease;
}

.tech-link:hover {
  background: rgba(16, 185, 129, 0.1);
  border-color: rgba(16, 185, 129, 0.3);
  color: var(--color-primary-light);
  transform: translateY(-2px);
}

.link-icon {
  opacity: 0;
  transition: opacity 0.3s ease;
}

.tech-link:hover .link-icon {
  opacity: 1;
}

.footer-divider {
  width: 60px;
  height: 2px;
  background: linear-gradient(90deg, transparent, var(--color-primary), transparent);
  margin: 32px auto;
}

.footer-bottom {
  text-align: center;
}

.copyright {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 6px;
  font-size: 0.9rem;
  color: var(--color-text-secondary);
  margin-bottom: 8px;
}

.heart-icon {
  color: #ef4444;
  animation: heartbeat 1.5s ease-in-out infinite;
}

@keyframes heartbeat {
  0%, 100% {
    transform: scale(1);
  }
  50% {
    transform: scale(1.2);
  }
}

.year {
  font-size: 0.8rem;
  color: var(--color-text-secondary);
  opacity: 0.7;
}

@media (max-width: 640px) {
  .tech-links {
    gap: 10px;
  }

  .tech-link {
    padding: 6px 12px;
    font-size: 0.8rem;
  }
}
</style>
