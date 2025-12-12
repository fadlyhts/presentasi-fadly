<script setup>
import { ref, onMounted, computed } from 'vue'
import { ExternalLink, Github, X, ChevronLeft, ChevronRight } from 'lucide-vue-next'

const isVisible = ref(false)
const selectedProject = ref(null)
const currentImageIndex = ref(0)

const projects = [
  {
    id: 1,
    title: 'PICA Kateko',
    description: 'Sistem monitoring kinerja pabrik teh dengan Dashboard Eksekutif, Self Assessment, dan Problem Identification & Corrective Action.',
    longDescription: 'Mengembangkan modul Off Farm Teh pada sistem PICA KATEKO Holding, meliputi Dashboard Eksekutif, Self Assessment Pabrik Teh, Problem Identification, dan Corrective Action untuk monitoring kinerja pabrik teh. Membangun fitur analisis Zona Kuadran, Klusterisasi, dan Ranking Pabrik Teh untuk evaluasi performa produk teh.',
    technologies: ['Laravel 12', 'Vue.js 3', 'Inertia.js', 'Tailwind CSS', 'ApexCharts', 'Leaflet Maps', 'MySQL'],
    images: [
      '/projects/pica/dashboard.png',
      '/projects/pica/informasi.png',
      '/projects/pica/dashboardeksekutif.png',
      '/projects/pica/petapabrik.png',
      '/projects/pica/kinerjapabrik.png',
      '/projects/pica/klusterisasipica.png',
      '/projects/pica/zonakuadran.png',
      '/projects/pica/rankpabrik.png',
      '/projects/pica/problem-identification.png',
      '/projects/pica/problem-identification2.png',
      '/projects/pica/correctiveaction.png',
      '/projects/pica/rata-rata-tertimbang.png',
      '/projects/pica/sentimenproduk.png'
    ],
    link: 'https://picakateko.holding-perkebunan.com/',
    color: '#10b981'
  },
  {
    id: 2,
    title: 'Aset Divestasi (Monika)',
    description: 'Continuous improvement sistem pengelolaan aset divestasi: migrasi Bootstrap, responsive design, fitur Export Excel, dan Soft Delete.',
    longDescription: `Continuous Improvement pada sistem pengelolaan aset divestasi berbasis CodeIgniter 4 dengan Bootstrap:
• Framework Migration: Migrasi dari Bootstrap 4 ke Bootstrap 5 untuk meningkatkan performa, memanfaatkan utility classes terbaru, dan memperbaiki tampilan komponen UI.
• History Tracking: Menampilkan riwayat RKAP (Rencana Kerja Anggaran Perusahaan) dan Non-RKAP pada halaman Detail Aset tab Progress Divest untuk transparansi dan audit trail.
• Responsive Design: Optimasi tampilan agar menyesuaikan berbagai ukuran device (desktop, tablet, mobile) dengan layout yang adaptif.
• Bug Fixing - Popup/Notifikasi: Memperbaiki sistem popup dan notifikasi agar tampil dengan benar dan memberikan feedback yang tepat kepada pengguna.
• Bug Fixing - Persentase Progress: Memperbaiki kalkulasi persentase yang tidak terupdate saat checkbox di-check atau uncheck pada tab Progress Divestasi.
• Multiselect Approval: Menambahkan fitur multiselect pada halaman Detail Aset untuk mempermudah proses approval multiple item sekaligus.
• User Feedback Enhancement: Menambahkan alert/response setelah pengguna mengklik button registrasi untuk memberikan konfirmasi aksi.
• Export Excel: Mengimplementasikan fitur download list objek yang sudah difilter ke dalam format file Excel menggunakan PHPSpreadsheet.
• Soft Delete: Menambahkan fitur soft delete objek sehingga data tidak terhapus permanen dan dapat di-restore jika diperlukan.`,
    technologies: ['CodeIgniter 4', 'Bootstrap 5', 'MySQL', 'PHPSpreadsheet', 'jQuery'],
    images: [
      '/projects/divestasi/gambar1.png',
      '/projects/divestasi/gambar2.png',
      '/projects/divestasi/gambar3.png',
      '/projects/divestasi/gambar4.png',
      '/projects/divestasi/gambar5.png',
      '/projects/divestasi/gambar6.png',
      '/projects/divestasi/gambar7.png'
    ],
    link: 'https://aset-dives-dev.ptpn1.co.id/',
    color: '#06b6d4'
  },
  {
    id: 3,
    title: 'Chatbot AI RAG WhatsApp',
    description: 'Sistem chatbot WhatsApp cerdas yang dapat menjawab pertanyaan berdasarkan dokumen-dokumen perusahaan secara otomatis.',
    longDescription: `Chatbot AI berbasis WhatsApp yang mampu menjawab pertanyaan pengguna secara cerdas berdasarkan dokumen-dokumen yang telah diunggah ke sistem.
• Cara Kerja: Pengguna cukup mengirim pertanyaan via WhatsApp, dan chatbot akan mencari jawaban yang relevan dari database dokumen, kemudian menyusun jawaban yang mudah dipahami.
• Mendukung Berbagai Format: Sistem dapat membaca dan memahami dokumen PDF, Word (DOCX), bahkan gambar dokumen melalui teknologi OCR (pengenalan teks dari gambar).
• Dashboard Admin: Tersedia halaman admin untuk mengelola dokumen, melihat statistik penggunaan chatbot, dan memantau riwayat percakapan.
• Integrasi WhatsApp: Terhubung langsung dengan WhatsApp sehingga karyawan dapat bertanya kapan saja melalui aplikasi yang sudah familiar.
• Pemrosesan di Latar Belakang: Dokumen besar diproses secara otomatis di background tanpa mengganggu kinerja sistem utama.`,
    technologies: ['Python', 'FastAPI', 'LangChain', 'Vue 3', 'TypeScript', 'Qdrant', 'Docker', 'Redis'],
    images: [
      '/projects/chatbot/dashboard.png',
      '/projects/chatbot/documents.png',
      '/projects/chatbot/chat1.png',
      '/projects/chatbot/chat2.png'
    ],
    link: null,
    color: '#8b5cf6'
  },
  {
    id: 4,
    title: 'SI-BAKTI',
    description: 'Aplikasi web fullstack untuk pengelolaan dokumen penyidikan dengan manajemen Laporan Polisi dan Berita Acara.',
    longDescription: 'Aplikasi web fullstack untuk pengelolaan dokumen penyidikan yang mencakup manajemen Laporan Polisi, Surat Perintah Penyidikan, Berita Acara, dan Aset. Dilengkapi fitur upload & preview dokumen PDF serta sistem autentikasi dengan role-based access control.',
    technologies: ['React', 'Vite', 'Express.js', 'MySQL'],
    images: [
      '/projects/sibakti/login.png',
      '/projects/sibakti/lp.png',
      '/projects/sibakti/sprindik.png',
      '/projects/sibakti/beritaacara.png',
      '/projects/sibakti/aset.png'
    ],
    link: null,
    color: '#f59e0b'
  },
  {
    id: 5,
    title: 'Rubber Leaf Disease API',
    description: 'RESTful API untuk identifikasi penyakit daun karet menggunakan model ConvNextV2 dan rekomendasi dari Google Gemini.',
    longDescription: 'Fine-tuned model ConvNextV2 untuk mengidentifikasi penyakit daun karet. RESTful API menggunakan FastAPI dengan integrasi Google Gemini API untuk memberikan rekomendasi penanganan yang relevan. Deployed menggunakan Docker.',
    technologies: ['Python', 'FastAPI', 'ConvNextV2', 'Google Gemini', 'Docker'],
    images: [],
    link: null,
    color: '#ec4899'
  }
]

const preloadImages = (images) => {
  images.forEach(src => {
    const img = new Image()
    img.src = src
  })
}

const openModal = (project) => {
  selectedProject.value = project
  currentImageIndex.value = 0
  document.body.style.overflow = 'hidden'
  
  // Preload all images for faster navigation
  if (project.images && project.images.length > 0) {
    preloadImages(project.images)
  }
}

const closeModal = () => {
  selectedProject.value = null
  currentImageIndex.value = 0
  document.body.style.overflow = 'auto'
}

const nextImage = () => {
  if (selectedProject.value && selectedProject.value.images.length > 0) {
    currentImageIndex.value = (currentImageIndex.value + 1) % selectedProject.value.images.length
  }
}

const prevImage = () => {
  if (selectedProject.value && selectedProject.value.images.length > 0) {
    currentImageIndex.value = currentImageIndex.value === 0 
      ? selectedProject.value.images.length - 1 
      : currentImageIndex.value - 1
  }
}

const goToImage = (index) => {
  currentImageIndex.value = index
}

onMounted(() => {
  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          isVisible.value = true
        }
      })
    },
    { threshold: 0.1 }
  )

  const section = document.querySelector('#projects')
  if (section) observer.observe(section)
})
</script>

<template>
  <section id="projects" class="section">
    <div class="container">
      <h2 class="section-title">
        <span class="gradient-text">Projects</span>
      </h2>
      <p class="section-subtitle">
        Proyek-proyek yang dikerjakan selama program magang
      </p>

      <div class="projects-grid" :class="{ 'visible': isVisible }">
        <div 
          v-for="(project, index) in projects" 
          :key="project.id"
          class="project-card glass-card"
          :style="{ '--delay': index * 0.1 + 's', '--accent-color': project.color }"
          @click="openModal(project)"
        >
          <!-- Project Image/Placeholder -->
          <div class="project-image">
            <img 
              v-if="project.images && project.images.length > 0" 
              :src="project.images[0]" 
              :alt="project.title"
              class="project-img"
            />
            <div 
              v-else 
              class="project-placeholder" 
              :style="{ background: `linear-gradient(135deg, ${project.color}30, ${project.color}10)` }"
            >
              <span class="project-number">{{ String(project.id).padStart(2, '0') }}</span>
            </div>
          </div>

          <!-- Project Info -->
          <div class="project-content">
            <h3 class="project-title">{{ project.title }}</h3>
            <p class="project-description">{{ project.description }}</p>
            
            <div class="project-tech">
              <span 
                v-for="tech in project.technologies.slice(0, 3)" 
                :key="tech" 
                class="tech-tag"
              >
                {{ tech }}
              </span>
              <span v-if="project.technologies.length > 3" class="tech-more">
                +{{ project.technologies.length - 3 }}
              </span>
            </div>

            <div class="project-footer">
              <span class="view-details">View Details</span>
              <ExternalLink :size="16" />
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Project Modal -->
    <Teleport to="body">
      <Transition name="modal">
        <div v-if="selectedProject" class="modal-overlay" @click.self="closeModal">
          <div class="modal-content glass-card">
            <button class="modal-close" @click="closeModal">
              <X :size="24" />
            </button>

            <!-- Image Carousel -->
            <div class="modal-carousel">
              <!-- If has images, show carousel -->
              <template v-if="selectedProject.images && selectedProject.images.length > 0">
                <div class="carousel-container">
                  <img 
                    :src="selectedProject.images[currentImageIndex]" 
                    :alt="`${selectedProject.title} screenshot ${currentImageIndex + 1}`"
                    class="carousel-image"
                  />
                  
                  <!-- Navigation Arrows -->
                  <button 
                    v-if="selectedProject.images.length > 1"
                    class="carousel-btn carousel-prev" 
                    @click="prevImage"
                  >
                    <ChevronLeft :size="24" />
                  </button>
                  <button 
                    v-if="selectedProject.images.length > 1"
                    class="carousel-btn carousel-next" 
                    @click="nextImage"
                  >
                    <ChevronRight :size="24" />
                  </button>
                  
                  <!-- Dot Indicators -->
                  <div v-if="selectedProject.images.length > 1" class="carousel-dots">
                    <button 
                      v-for="(_, index) in selectedProject.images" 
                      :key="index"
                      class="carousel-dot"
                      :class="{ active: currentImageIndex === index }"
                      @click="goToImage(index)"
                    />
                  </div>
                </div>
              </template>
              
              <!-- Placeholder if no images -->
              <template v-else>
                <div 
                  class="modal-placeholder" 
                  :style="{ background: `linear-gradient(135deg, ${selectedProject.color}40, ${selectedProject.color}10)` }"
                >
                  <span class="modal-number">{{ String(selectedProject.id).padStart(2, '0') }}</span>
                </div>
              </template>
            </div>

            <div class="modal-body">
              <h3 class="modal-title">{{ selectedProject.title }}</h3>
              <p class="modal-description">{{ selectedProject.longDescription }}</p>

              <div class="modal-section">
                <h4>Technologies Used</h4>
                <div class="modal-tech">
                  <span 
                    v-for="tech in selectedProject.technologies" 
                    :key="tech" 
                    class="modal-tech-tag"
                    :style="{ borderColor: selectedProject.color }"
                  >
                    {{ tech }}
                  </span>
                </div>
              </div>

              <div class="modal-actions">
                <a 
                  v-if="selectedProject.link" 
                  :href="selectedProject.link" 
                  target="_blank"
                  class="modal-btn primary" 
                  :style="{ background: selectedProject.color }"
                >
                  <ExternalLink :size="18" />
                  Live Demo
                </a>
                <a href="#" class="modal-btn secondary">
                  <Github :size="18" />
                  View Code
                </a>
              </div>
            </div>
          </div>
        </div>
      </Transition>
    </Teleport>
  </section>
</template>

<style scoped>
.projects-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 24px;
  opacity: 0;
}

.projects-grid.visible {
  opacity: 1;
}

.projects-grid.visible .project-card {
  animation: fadeInUp 0.6s ease forwards;
  animation-delay: var(--delay);
}

.project-card {
  cursor: pointer;
  overflow: hidden;
  transition: all 0.3s ease;
  opacity: 0;
}

.project-card:hover {
  transform: translateY(-8px);
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.3);
  border-color: var(--accent-color);
}

.project-image {
  position: relative;
  height: 180px;
  overflow: hidden;
}

.project-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.3s ease;
}

.project-card:hover .project-img {
  transform: scale(1.05);
}

.project-placeholder {
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: transform 0.3s ease;
}

.project-card:hover .project-placeholder {
  transform: scale(1.05);
}

.project-number {
  font-size: 4rem;
  font-weight: 800;
  color: rgba(255, 255, 255, 0.1);
}

.project-content {
  padding: 24px;
}

.project-title {
  font-size: 1.15rem;
  font-weight: 700;
  margin-bottom: 12px;
  color: var(--color-text-primary);
}

.project-description {
  font-size: 0.9rem;
  color: var(--color-text-secondary);
  line-height: 1.6;
  margin-bottom: 16px;
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

.project-tech {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
  margin-bottom: 16px;
}

.tech-tag {
  background: rgba(148, 163, 184, 0.1);
  padding: 4px 10px;
  border-radius: 4px;
  font-size: 0.75rem;
  color: var(--color-text-secondary);
}

.tech-more {
  font-size: 0.75rem;
  color: var(--color-primary);
  font-weight: 600;
}

.project-footer {
  display: flex;
  align-items: center;
  gap: 8px;
  color: var(--accent-color);
  font-size: 0.85rem;
  font-weight: 500;
  transition: gap 0.3s ease;
}

.project-card:hover .project-footer {
  gap: 12px;
}

/* Modal Styles */
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.85);
  backdrop-filter: blur(10px);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
  padding: 24px;
}

.modal-content {
  max-width: 900px;
  width: 100%;
  max-height: 90vh;
  overflow-y: auto;
  position: relative;
}

.modal-close {
  position: absolute;
  top: 16px;
  right: 16px;
  background: rgba(0, 0, 0, 0.5);
  border: none;
  border-radius: 50%;
  width: 44px;
  height: 44px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  cursor: pointer;
  transition: all 0.3s ease;
  z-index: 10;
}

.modal-close:hover {
  background: rgba(0, 0, 0, 0.7);
  transform: rotate(90deg);
}

/* Carousel Styles */
.modal-carousel {
  position: relative;
  width: 100%;
  height: 550px;
  border-radius: 16px 16px 0 0;
  overflow: hidden;
}

.carousel-container {
  position: relative;
  width: 100%;
  height: 100%;
}

.carousel-image {
  width: 100%;
  height: 100%;
  object-fit: contain;
  background: #1a1a2e;
  transition: opacity 0.3s ease;
}

.carousel-btn {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  background: rgba(0, 0, 0, 0.6);
  border: none;
  border-radius: 50%;
  width: 48px;
  height: 48px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  cursor: pointer;
  transition: all 0.3s ease;
}

.carousel-btn:hover {
  background: rgba(0, 0, 0, 0.8);
  transform: translateY(-50%) scale(1.1);
}

.carousel-prev {
  left: 16px;
}

.carousel-next {
  right: 16px;
}

.carousel-dots {
  position: absolute;
  bottom: 16px;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  gap: 8px;
}

.carousel-dot {
  width: 10px;
  height: 10px;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.4);
  border: none;
  cursor: pointer;
  transition: all 0.3s ease;
}

.carousel-dot:hover {
  background: rgba(255, 255, 255, 0.7);
}

.carousel-dot.active {
  background: white;
  transform: scale(1.2);
}

.modal-placeholder {
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 16px 16px 0 0;
}

.modal-number {
  font-size: 6rem;
  font-weight: 800;
  color: rgba(0, 0, 0, 0.1);
}

.modal-body {
  padding: 32px;
}

.modal-title {
  font-size: 1.5rem;
  font-weight: 700;
  margin-bottom: 16px;
}

.modal-description {
  color: var(--color-text-secondary);
  line-height: 1.8;
  margin-bottom: 24px;
  white-space: pre-line;
}

.modal-section {
  margin-bottom: 24px;
}

.modal-section h4 {
  font-size: 0.9rem;
  font-weight: 600;
  color: var(--color-text-secondary);
  margin-bottom: 12px;
  text-transform: uppercase;
  letter-spacing: 0.05em;
}

.modal-tech {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
}

.modal-tech-tag {
  background: rgba(148, 163, 184, 0.1);
  border: 1px solid;
  padding: 6px 14px;
  border-radius: 6px;
  font-size: 0.85rem;
  color: var(--color-text-primary);
}

.modal-actions {
  display: flex;
  gap: 12px;
}

.modal-btn {
  display: flex;
  align-items: center;
  gap: 8px;
  padding: 12px 24px;
  border-radius: 8px;
  font-size: 0.9rem;
  font-weight: 600;
  text-decoration: none;
  transition: all 0.3s ease;
}

.modal-btn.primary {
  color: white;
}

.modal-btn.primary:hover {
  filter: brightness(1.1);
  transform: translateY(-2px);
}

.modal-btn.secondary {
  background: rgba(148, 163, 184, 0.1);
  color: var(--color-text-primary);
  border: 1px solid var(--color-border);
}

.modal-btn.secondary:hover {
  background: rgba(148, 163, 184, 0.2);
}

/* Modal Transition */
.modal-enter-active,
.modal-leave-active {
  transition: all 0.3s ease;
}

.modal-enter-from,
.modal-leave-to {
  opacity: 0;
}

.modal-enter-from .modal-content,
.modal-leave-to .modal-content {
  transform: scale(0.9);
}

@media (max-width: 1024px) {
  .projects-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 640px) {
  .projects-grid {
    grid-template-columns: 1fr;
  }

  .modal-actions {
    flex-direction: column;
  }

  .modal-body {
    padding: 24px;
  }
}
</style>
