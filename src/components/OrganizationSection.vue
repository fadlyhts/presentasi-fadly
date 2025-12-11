<script setup>
import { ref, onMounted } from 'vue'
import { Users } from 'lucide-vue-next'

const isVisible = ref(false)

onMounted(() => {
  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          isVisible.value = true
        }
      })
    },
    { threshold: 0.2 }
  )

  const section = document.querySelector('#organisasi')
  if (section) observer.observe(section)
})
</script>

<template>
  <section id="organisasi" class="section">
    <div class="container">
      <h2 class="section-title">
        <span class="gradient-text">Struktur Organisasi</span>
      </h2>
      <p class="section-subtitle">
        Divisi Pengadaan dan Teknologi Informasi
      </p>

      <div class="org-wrapper" :class="{ 'visible': isVisible }">
        <!-- Level 1: Kepala Divisi -->
        <div class="org-level org-level-1">
          <div class="org-card org-card-head glass-card">
            <div class="org-icon">
              <Users :size="28" />
            </div>
            <h3 class="org-title">Kepala Divisi Pengadaan dan Teknologi Informasi</h3>
          </div>
        </div>

        <!-- Connector Line -->
        <div class="org-connector">
          <div class="connector-vertical"></div>
          <div class="connector-horizontal"></div>
        </div>

        <!-- Level 2: Sub Divisi -->
        <div class="org-level org-level-2">
          <div class="org-card-wrapper">
            <div class="card-connector"></div>
            <div class="org-card glass-card">
              <div class="org-icon org-icon-sm">
                <Users :size="22" />
              </div>
              <h3 class="org-title">Kepala Sub Divisi Pengadaan</h3>
            </div>
          </div>
          
          <div class="org-card-with-sub">
            <div class="card-connector"></div>
            <div class="org-card glass-card highlighted">
              <div class="org-icon org-icon-sm">
                <Users :size="22" />
              </div>
              <h3 class="org-title">Kepala Sub Divisi Tata Kelola dan Pengembangan TI</h3>
            </div>
            
            <!-- Connector to Asisten -->
            <div class="sub-connector">
              <div class="connector-vertical-sm"></div>
            </div>
            
            <!-- Level 3: Asisten -->
            <div class="org-card org-card-asisten glass-card">
              <div class="org-icon org-icon-xs">
                <Users :size="18" />
              </div>
              <h3 class="org-title">Asisten Pengembangan TI</h3>
            </div>
          </div>
          
          <div class="org-card-wrapper">
            <div class="card-connector"></div>
            <div class="org-card glass-card">
              <div class="org-icon org-icon-sm">
                <Users :size="22" />
              </div>
              <h3 class="org-title">Kepala Sub Divisi Pemetaan dan GIS</h3>
            </div>
          </div>
          
          <div class="org-card-wrapper">
            <div class="card-connector"></div>
            <div class="org-card glass-card">
              <div class="org-icon org-icon-sm">
                <Users :size="22" />
              </div>
              <h3 class="org-title">Kepala Sub Divisi Operasional TI & ERP</h3>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.org-wrapper {
  max-width: 1100px;
  margin: 0 auto;
  opacity: 0;
  transform: translateY(40px);
  transition: all 0.8s cubic-bezier(0.16, 1, 0.3, 1);
}

.org-wrapper.visible {
  opacity: 1;
  transform: translateY(0);
}

.org-level {
  display: flex;
  justify-content: center;
  gap: 20px;
}

.org-level-1 {
  margin-bottom: 0;
}

.org-level-2 {
  align-items: flex-start;
  position: relative;
}

.org-card-wrapper,
.org-card-with-sub {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.card-connector {
  width: 2px;
  height: 20px;
  background: var(--color-primary);
}

.org-connector {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 100%;
  position: relative;
}

.connector-vertical {
  width: 2px;
  height: 20px;
  background: var(--color-primary);
}

.connector-horizontal {
  width: calc(100% - 200px);
  max-width: 820px;
  height: 2px;
  background: var(--color-primary);
}

.org-card {
  padding: 20px;
  text-align: center;
  transition: all 0.3s ease;
  min-width: 200px;
  max-width: 220px;
}

.org-card:hover {
  transform: translateY(-4px);
  box-shadow: 0 10px 30px rgba(16, 185, 129, 0.15);
}

.org-card-head {
  min-width: 350px;
  max-width: 400px;
  padding: 24px 32px;
  border: 2px solid var(--color-primary);
}

.org-card.highlighted {
  border: 2px solid var(--color-primary);
  background: rgba(16, 185, 129, 0.05);
}

.org-card-with-sub {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.sub-connector {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.connector-vertical-sm {
  width: 2px;
  height: 20px;
  background: var(--color-primary);
}

.org-card-asisten {
  min-width: 180px;
  max-width: 200px;
  padding: 16px;
  background: rgba(16, 185, 129, 0.08);
  border: 1px dashed var(--color-primary);
}

.org-icon {
  width: 50px;
  height: 50px;
  border-radius: 12px;
  background: linear-gradient(135deg, var(--color-primary), var(--color-primary-dark));
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  margin: 0 auto 12px;
}

.org-icon-sm {
  width: 42px;
  height: 42px;
}

.org-icon-xs {
  width: 36px;
  height: 36px;
}

.org-title {
  font-size: 0.85rem;
  font-weight: 600;
  color: var(--color-text-primary);
  line-height: 1.4;
}

.org-card-head .org-title {
  font-size: 1rem;
  font-weight: 700;
}

.org-card-asisten .org-title {
  font-size: 0.8rem;
}

@media (max-width: 1024px) {
  .org-level-2 {
    flex-wrap: wrap;
    gap: 16px;
  }
  
  .org-card {
    min-width: 180px;
    max-width: 200px;
  }
  
  .connector-horizontal {
    width: 60%;
  }
}

@media (max-width: 768px) {
  .org-level-2 {
    flex-direction: column;
    align-items: center;
  }
  
  .org-card {
    min-width: 280px;
    max-width: 300px;
  }
  
  .org-card-head {
    min-width: 280px;
    max-width: 300px;
  }
  
  .connector-horizontal {
    display: none;
  }
  
  .org-connector {
    height: 30px;
  }
  
  .connector-vertical {
    height: 30px;
  }
}
</style>
