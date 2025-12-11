<script setup>
import { ref, onMounted } from 'vue'
import { Menu, X } from 'lucide-vue-next'

// Import logos
import logoPtpn1 from '@/assets/logo/logo_ptpn1.png'
import logoHolding from '@/assets/logo/logo_holding.png'
import logoDanantara from '@/assets/logo/logo_danantara.webp'
import logoFhci from '@/assets/logo/logo_fhci.png'
import logoMagenta from '@/assets/logo/logo_magenta.png'

const isMenuOpen = ref(false)
const isScrolled = ref(false)

const navLinks = [
  { name: 'Home', href: '#home' },
  { name: 'Profil', href: '#profil' },
  { name: 'Organisasi', href: '#organisasi' },
  { name: 'Projects', href: '#projects' }
]

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value
}

const scrollToSection = (href) => {
  const element = document.querySelector(href)
  if (element) {
    element.scrollIntoView({ behavior: 'smooth' })
    isMenuOpen.value = false
  }
}

onMounted(() => {
  window.addEventListener('scroll', () => {
    isScrolled.value = window.scrollY > 50
  })
})
</script>

<template>
  <nav 
    class="navbar" 
    :class="{ 'navbar-scrolled': isScrolled }"
  >
    <div class="navbar-container">
      <!-- Left Logos -->
      <div class="navbar-logos navbar-logos-left">
        <img :src="logoPtpn1" alt="PTPN 1" class="nav-logo" />
        <img :src="logoHolding" alt="Holding Perkebunan" class="nav-logo" />
        <img :src="logoDanantara" alt="Danantara" class="nav-logo" />
      </div>

      <!-- Desktop Navigation -->
      <div class="navbar-links">
        <a 
          v-for="link in navLinks" 
          :key="link.name"
          :href="link.href"
          class="navbar-link"
          @click.prevent="scrollToSection(link.href)"
        >
          {{ link.name }}
        </a>
      </div>

      <!-- Right Logos -->
      <div class="navbar-logos navbar-logos-right">
        <img :src="logoFhci" alt="FHCI" class="nav-logo" />
        <img :src="logoMagenta" alt="Magenta" class="nav-logo" />
      </div>

      <!-- Mobile Menu Button -->
      <button class="navbar-toggle" @click="toggleMenu">
        <Menu v-if="!isMenuOpen" :size="24" />
        <X v-else :size="24" />
      </button>
    </div>

    <!-- Mobile Navigation -->
    <div class="navbar-mobile" :class="{ 'navbar-mobile-open': isMenuOpen }">
      <a 
        v-for="link in navLinks" 
        :key="link.name"
        :href="link.href"
        class="navbar-mobile-link"
        @click.prevent="scrollToSection(link.href)"
      >
        {{ link.name }}
      </a>
    </div>
  </nav>
</template>

<style scoped>
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 100;
  padding: 16px 24px;
  transition: all 0.3s ease;
}

.navbar-scrolled {
  background: rgba(255, 255, 255, 0.95);
  backdrop-filter: blur(20px);
  border-bottom: 1px solid rgba(148, 163, 184, 0.2);
  box-shadow: 0 2px 20px rgba(0, 0, 0, 0.08);
  padding: 12px 24px;
}

.navbar-container {
  max-width: 1400px;
  margin: 0 auto;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 24px;
}

.navbar-logos {
  display: flex;
  align-items: center;
  gap: 12px;
}

.nav-logo {
  height: 40px;
  width: auto;
  object-fit: contain;
}

.navbar-links {
  display: flex;
  gap: 32px;
}

.navbar-link {
  color: var(--color-text-secondary);
  text-decoration: none;
  font-weight: 500;
  font-size: 0.95rem;
  transition: color 0.3s ease;
  position: relative;
}

.navbar-link::after {
  content: '';
  position: absolute;
  bottom: -4px;
  left: 0;
  width: 0;
  height: 2px;
  background: var(--color-primary);
  transition: width 0.3s ease;
}

.navbar-link:hover {
  color: var(--color-text-primary);
}

.navbar-link:hover::after {
  width: 100%;
}

.navbar-toggle {
  display: none;
  background: none;
  border: none;
  color: var(--color-text-primary);
  cursor: pointer;
  padding: 8px;
}

.navbar-mobile {
  display: none;
  flex-direction: column;
  gap: 16px;
  padding: 24px;
  max-height: 0;
  overflow: hidden;
  transition: max-height 0.3s ease;
}

.navbar-mobile-open {
  max-height: 300px;
}

.navbar-mobile-link {
  color: var(--color-text-secondary);
  text-decoration: none;
  font-weight: 500;
  font-size: 1.1rem;
  padding: 8px 0;
  transition: color 0.3s ease;
}

.navbar-mobile-link:hover {
  color: var(--color-primary);
}

@media (max-width: 768px) {
  .navbar-links {
    display: none;
  }

  .navbar-toggle {
    display: block;
  }

  .navbar-mobile {
    display: flex;
    background: rgba(255, 255, 255, 0.98);
  }

  .navbar-logos-right {
    display: none;
  }

  .nav-logo {
    height: 28px;
  }

  .navbar-logos-left {
    gap: 8px;
  }
}
</style>

