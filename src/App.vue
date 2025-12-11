<script setup>
import Navbar from './components/Navbar.vue'
import HeroSection from './components/HeroSection.vue'
import ProfileSection from './components/ProfileSection.vue'
import OrganizationSection from './components/OrganizationSection.vue'
import ProjectsSection from './components/ProjectsSection.vue'
import Footer from './components/Footer.vue'
</script>

<template>
  <div class="app">
    <!-- Navigation -->
    <Navbar />
    
    <!-- Main Content -->
    <main>
      <HeroSection />
      <ProfileSection />
      <OrganizationSection />
      <ProjectsSection />
    </main>
    
    <!-- Footer -->
    <Footer />
  </div>
</template>

<style>
.app {
  position: relative;
  min-height: 100vh;
}
</style>
