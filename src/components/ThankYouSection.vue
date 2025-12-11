<script setup>
import { ref } from 'vue'
import { Heart, Sparkles } from 'lucide-vue-next'

const isExploding = ref(false)
const particles = ref([])

const triggerExplosion = () => {
  isExploding.value = true
  particles.value = []
  
  // Create particles
  const emojis = ['🌸', '🌺', '🌷', '💐', '🌻', '🌹', '✨', '⭐', '💫', '🎉', '🎊', '💖']
  
  for (let i = 0; i < 150; i++) {
    particles.value.push({
      id: i,
      emoji: emojis[Math.floor(Math.random() * emojis.length)],
      x: Math.random() * 100,
      y: Math.random() * 100,
      delay: Math.random() * 0.5,
      duration: 1 + Math.random() * 2,
      size: 1 + Math.random() * 1.5
    })
  }
  
  // Reset after animation
  setTimeout(() => {
    isExploding.value = false
    particles.value = []
  }, 3000)
}
</script>

<template>
  <section id="thankyou" class="section thankyou-section">
    <div class="container">
      <div class="thankyou-content">
        <div class="thankyou-icon">
          <Sparkles :size="48" />
        </div>
        
        <h2 class="thankyou-title">
          <span class="gradient-text">Terima Kasih</span>
        </h2>
        
        <p class="thankyou-subtitle">
          Atas perhatian dan kesempatan yang telah diberikan
        </p>
        
        <button class="celebration-btn" @click="triggerExplosion" :disabled="isExploding">
          <Heart :size="20" />
          <span>{{ isExploding ? 'Celebrating!' : 'Celebrate 🎉' }}</span>
        </button>
      </div>
      
      <!-- Particle Explosion -->
      <div v-if="isExploding" class="particles-container">
        <span 
          v-for="particle in particles" 
          :key="particle.id"
          class="particle"
          :style="{
            left: `${particle.x}%`,
            top: `${particle.y}%`,
            animationDelay: `${particle.delay}s`,
            animationDuration: `${particle.duration}s`,
            fontSize: `${particle.size}rem`
          }"
        >
          {{ particle.emoji }}
        </span>
      </div>
    </div>
  </section>
</template>

<style scoped>
.thankyou-section {
  position: relative;
  overflow: hidden;
  min-height: 60vh;
  display: flex;
  align-items: center;
  justify-content: center;
}

.thankyou-content {
  text-align: center;
  position: relative;
  z-index: 2;
}

.thankyou-icon {
  width: 80px;
  height: 80px;
  margin: 0 auto 24px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: linear-gradient(135deg, var(--color-primary), #34d399);
  border-radius: 50%;
  color: white;
  animation: pulse 2s ease-in-out infinite;
}

@keyframes pulse {
  0%, 100% { transform: scale(1); }
  50% { transform: scale(1.1); }
}

.thankyou-title {
  font-size: 3rem;
  font-weight: 800;
  margin-bottom: 16px;
}

.thankyou-subtitle {
  font-size: 1.2rem;
  color: var(--color-text-secondary);
  margin-bottom: 40px;
  max-width: 500px;
  margin-left: auto;
  margin-right: auto;
}

.celebration-btn {
  display: inline-flex;
  align-items: center;
  gap: 10px;
  padding: 16px 40px;
  font-size: 1.1rem;
  font-weight: 600;
  color: white;
  background: linear-gradient(135deg, var(--color-primary), #34d399);
  border: none;
  border-radius: 50px;
  cursor: pointer;
  transition: all 0.3s ease;
  box-shadow: 0 4px 20px rgba(16, 185, 129, 0.4);
}

.celebration-btn:hover:not(:disabled) {
  transform: translateY(-3px);
  box-shadow: 0 8px 30px rgba(16, 185, 129, 0.5);
}

.celebration-btn:disabled {
  opacity: 0.8;
  cursor: default;
}

/* Particles */
.particles-container {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
  z-index: 9999;
}

.particle {
  position: absolute;
  animation: explode ease-out forwards;
}

@keyframes explode {
  0% {
    opacity: 1;
    transform: scale(0) translateY(0);
  }
  50% {
    opacity: 1;
  }
  100% {
    opacity: 0;
    transform: scale(1) translateY(-200px) rotate(720deg);
  }
}

@media (max-width: 768px) {
  .thankyou-title {
    font-size: 2.2rem;
  }
  
  .thankyou-subtitle {
    font-size: 1rem;
  }
  
  .celebration-btn {
    padding: 14px 32px;
    font-size: 1rem;
  }
}
</style>
