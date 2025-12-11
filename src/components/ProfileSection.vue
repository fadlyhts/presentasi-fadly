<script setup>
import { ref, onMounted } from 'vue'
import { Briefcase, GraduationCap, Mail } from 'lucide-vue-next'
import profilePhoto from '@/assets/fadly.jpg'

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

  const section = document.querySelector('#profil')
  if (section) observer.observe(section)
})
</script>

<template>
  <section id="profil" class="section">
    <div class="container">
      <h2 class="section-title">
        <span class="gradient-text">Profil</span>
      </h2>


      <div class="profile-wrapper" :class="{ 'visible': isVisible }">
        <!-- Profile Card -->
        <div class="profile-card glass-card">
          <div class="profile-avatar">
            <img :src="profilePhoto" alt="Fadly" class="avatar-image" />
          </div>
          <h3 class="profile-name">Ahmad Fadli Hutasuhut</h3>
          
          <div class="profile-divider"></div>

          <div class="profile-info">
            <div class="info-item">
              <GraduationCap :size="20" class="info-icon" />
              <span>Universitas Negeri Jakarta</span>
            </div>
            <div class="info-item">
              <Briefcase :size="20" class="info-icon" />
              <span>DPTI</span>
            </div>
            <div class="info-item">
              <Mail :size="20" class="info-icon" />
              <span>fadly@fadlyhts.my.id</span>
            </div>
          </div>

          <div class="profile-divider"></div>

          <!-- Skills -->
          <div class="profile-skills">
            <h4 class="skills-title">Skills</h4>
            <div class="skills-list">
              <span class="skill-tag">JavaScript</span>
              <span class="skill-tag">TypeScript</span>
              <span class="skill-tag">React</span>
              <span class="skill-tag">Vue.js</span>
              <span class="skill-tag">Express.js</span>
              <span class="skill-tag">Laravel</span>
              <span class="skill-tag">Python</span>
              <span class="skill-tag">FastAPI</span>
              <span class="skill-tag">Machine Learning</span>
              <span class="skill-tag">Artificial Intelligence</span>
              <span class="skill-tag">DevOps</span>
            </div>
          </div>
        </div>

        <!-- Pengalaman Card -->
        <div class="experience-card glass-card">
          <h4 class="experience-title">Pengalaman</h4>
          
          <div class="experience-list">
            <!-- PTPN I -->
            <div class="exp-item">
              <div class="exp-left">
                <span class="exp-date">Jul 2025 - Sekarang</span>
              </div>
              <div class="exp-right">
                <h5 class="exp-role">IT Development Intern</h5>
                <p class="exp-company">PT. Perkebunan Nusantara I</p>
                <p class="exp-desc">Dashboard PICA Kateko, Chatbot AI RAG WhatsApp, Sistem Aset Monika</p>
                <div class="exp-tags">
                  <span>Laravel</span>
                  <span>Vue.js</span>
                  <span>Python</span>
                  <span>FastAPI</span>
                </div>
              </div>
            </div>

            <!-- Agincourt -->
            <div class="exp-item">
              <div class="exp-left">
                <span class="exp-date">Apr - Jul 2025</span>
              </div>
              <div class="exp-right">
                <h5 class="exp-role">IT & Systems Intern</h5>
                <p class="exp-company">PT. Agincourt Resources</p>
                <p class="exp-desc">IT Support, Infrastruktur Jaringan, Sistem Penghitung Penumpang Berbasis IoT</p>
                <div class="exp-tags">
                  <span>React</span>
                  <span>Node.js</span>
                  <span>IoT</span>
                </div>
              </div>
            </div>

            <!-- Infinite Learning -->
            <div class="exp-item">
              <div class="exp-left">
                <span class="exp-date">Mar - Jul 2025</span>
              </div>
              <div class="exp-right">
                <h5 class="exp-role">AI Engineer</h5>
                <p class="exp-company">Infinite Learning Indonesia</p>
                <p class="exp-desc">Machine Learning, Deep Learning, NLP, Computer Vision, RAG dengan LLM</p>
                <div class="exp-tags">
                  <span>Python</span>
                  <span>TensorFlow</span>
                  <span>LangChain</span>
                </div>
              </div>
            </div>

            <!-- Dicoding -->
            <div class="exp-item">
              <div class="exp-left">
                <span class="exp-date">Sep - Des 2024</span>
              </div>
              <div class="exp-right">
                <h5 class="exp-role">Fullstack Web Developer</h5>
                <p class="exp-company">Dicoding x Kampus Merdeka</p>
                <p class="exp-desc">Komponen Web, RESTful APIs, PWA, Jakarta Park Finder</p>
                <div class="exp-tags">
                  <span>JavaScript</span>
                  <span>React</span>
                  <span>Express.js</span>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.profile-wrapper {
  display: grid;
  grid-template-columns: 1fr 2fr;
  gap: 32px;
  max-width: 1000px;
  margin: 0 auto;
  opacity: 0;
  transform: translateY(40px);
  transition: all 0.8s cubic-bezier(0.16, 1, 0.3, 1);
}

.profile-wrapper.visible {
  opacity: 1;
  transform: translateY(0);
}

.profile-card {
  padding: 40px 32px;
  text-align: center;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.profile-avatar {
  width: 140px;
  height: 140px;
  border-radius: 50%;
  overflow: hidden;
  margin-bottom: 24px;
  box-shadow: 0 4px 30px rgba(16, 185, 129, 0.25);
  border: 4px solid var(--color-primary);
}

.avatar-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.profile-name {
  font-size: 1.5rem;
  font-weight: 700;
  margin-bottom: 4px;
}

.profile-role {
  color: var(--color-primary-light);
  font-size: 0.95rem;
  font-weight: 500;
}

.profile-divider {
  width: 60px;
  height: 2px;
  background: linear-gradient(90deg, transparent, var(--color-primary), transparent);
  margin: 24px 0;
}

.profile-info {
  width: 100%;
}

.info-item {
  display: flex;
  align-items: center;
  gap: 12px;
  padding: 12px 0;
  color: var(--color-text-secondary);
  font-size: 0.9rem;
}

.info-icon {
  color: var(--color-primary);
}

.experience-card {
  padding: 32px;
}

.experience-title {
  font-size: 1.25rem;
  font-weight: 700;
  margin-bottom: 24px;
  color: var(--color-primary);
}

.experience-list {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.exp-item {
  display: grid;
  grid-template-columns: 140px 1fr;
  gap: 20px;
  padding-bottom: 20px;
  border-bottom: 1px solid var(--color-border);
}

.exp-item:last-child {
  border-bottom: none;
  padding-bottom: 0;
}

.exp-left {
  text-align: right;
}

.exp-date {
  font-size: 0.8rem;
  color: var(--color-primary);
  font-weight: 600;
  line-height: 1.6;
}

.exp-right {
  display: flex;
  flex-direction: column;
  gap: 4px;
}

.exp-role {
  font-size: 1rem;
  font-weight: 700;
  color: var(--color-text-primary);
  margin: 0;
}

.exp-company {
  font-size: 0.9rem;
  color: var(--color-text-secondary);
  font-weight: 500;
  margin: 0;
}

.exp-desc {
  font-size: 0.85rem;
  color: var(--color-text-secondary);
  line-height: 1.5;
  margin: 4px 0;
}

.exp-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 6px;
  margin-top: 8px;
}

.exp-tags span {
  font-size: 0.75rem;
  padding: 4px 10px;
  background: rgba(16, 185, 129, 0.1);
  border: 1px solid rgba(16, 185, 129, 0.25);
  border-radius: 4px;
  color: var(--color-primary);
  font-weight: 500;
}

@media (max-width: 768px) {
  .profile-wrapper {
    grid-template-columns: 1fr;
  }

  .profile-card {
    padding: 32px 24px;
  }

  .experience-card {
    padding: 24px 20px;
  }

  .exp-item {
    grid-template-columns: 1fr;
    gap: 8px;
  }

  .exp-left {
    text-align: left;
  }

  .exp-date {
    display: inline-block;
    background: rgba(16, 185, 129, 0.1);
    padding: 2px 10px;
    border-radius: 12px;
  }
}

/* Skills inside Profile Card */
.profile-skills {
  margin-top: 8px;
}

.skills-title {
  font-size: 1.1rem;
  font-weight: 700;
  color: var(--color-primary);
  margin-bottom: 16px;
}

.skills-list {
  display: flex;
  flex-wrap: wrap;
  gap: 6px;
}

.skill-tag {
  padding: 4px 10px;
  background: linear-gradient(135deg, rgba(16, 185, 129, 0.15), rgba(52, 211, 153, 0.1));
  border: 1px solid rgba(16, 185, 129, 0.3);
  border-radius: 12px;
  font-size: 0.7rem;
  font-weight: 500;
  color: var(--color-primary);
  transition: all 0.3s ease;
}

.skill-tag:hover {
  background: linear-gradient(135deg, rgba(16, 185, 129, 0.25), rgba(52, 211, 153, 0.2));
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(16, 185, 129, 0.2);
}
</style>
