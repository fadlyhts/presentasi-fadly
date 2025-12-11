<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import * as THREE from 'three'

const containerRef = ref(null)
let scene, camera, renderer, particles
let animationId

const initThree = () => {
  if (!containerRef.value) return

  // Scene setup
  scene = new THREE.Scene()
  
  // Camera setup
  camera = new THREE.PerspectiveCamera(
    75,
    window.innerWidth / window.innerHeight,
    0.1,
    1000
  )
  camera.position.z = 50

  // Renderer setup
  renderer = new THREE.WebGLRenderer({ 
    antialias: true, 
    alpha: true 
  })
  renderer.setSize(window.innerWidth, window.innerHeight)
  renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2))
  containerRef.value.appendChild(renderer.domElement)

  // Create particles
  createParticles()

  // Start animation
  animate()

  // Handle resize
  window.addEventListener('resize', onWindowResize)
}

const createParticles = () => {
  const geometry = new THREE.BufferGeometry()
  const count = 2000

  const positions = new Float32Array(count * 3)
  const colors = new Float32Array(count * 3)

  const color1 = new THREE.Color('#10b981') // Emerald
  const color2 = new THREE.Color('#06b6d4') // Cyan
  const color3 = new THREE.Color('#8b5cf6') // Purple

  for (let i = 0; i < count; i++) {
    const i3 = i * 3

    // Position - spread across screen
    positions[i3] = (Math.random() - 0.5) * 150
    positions[i3 + 1] = (Math.random() - 0.5) * 150
    positions[i3 + 2] = (Math.random() - 0.5) * 100

    // Colors - mix of emerald, cyan, and purple
    const mixedColor = new THREE.Color()
    const rand = Math.random()
    if (rand < 0.33) {
      mixedColor.copy(color1)
    } else if (rand < 0.66) {
      mixedColor.copy(color2)
    } else {
      mixedColor.copy(color3)
    }
    
    colors[i3] = mixedColor.r
    colors[i3 + 1] = mixedColor.g
    colors[i3 + 2] = mixedColor.b
  }

  geometry.setAttribute('position', new THREE.BufferAttribute(positions, 3))
  geometry.setAttribute('color', new THREE.BufferAttribute(colors, 3))

  // Material
  const material = new THREE.PointsMaterial({
    size: 0.5,
    sizeAttenuation: true,
    vertexColors: true,
    transparent: true,
    opacity: 0.8,
    blending: THREE.AdditiveBlending
  })

  particles = new THREE.Points(geometry, material)
  scene.add(particles)

  // Add connecting lines for a network effect
  createConnections()
}

const createConnections = () => {
  const geometry = new THREE.BufferGeometry()
  const lineCount = 100
  const positions = new Float32Array(lineCount * 6)

  for (let i = 0; i < lineCount; i++) {
    const i6 = i * 6

    positions[i6] = (Math.random() - 0.5) * 100
    positions[i6 + 1] = (Math.random() - 0.5) * 100
    positions[i6 + 2] = (Math.random() - 0.5) * 50

    positions[i6 + 3] = positions[i6] + (Math.random() - 0.5) * 30
    positions[i6 + 4] = positions[i6 + 1] + (Math.random() - 0.5) * 30
    positions[i6 + 5] = positions[i6 + 2] + (Math.random() - 0.5) * 20
  }

  geometry.setAttribute('position', new THREE.BufferAttribute(positions, 3))

  const material = new THREE.LineBasicMaterial({
    color: 0x10b981,
    transparent: true,
    opacity: 0.15
  })

  const lines = new THREE.LineSegments(geometry, material)
  scene.add(lines)
}

const animate = () => {
  animationId = requestAnimationFrame(animate)

  // Rotate particles slowly
  if (particles) {
    particles.rotation.x += 0.0003
    particles.rotation.y += 0.0005
  }

  renderer.render(scene, camera)
}

const onWindowResize = () => {
  camera.aspect = window.innerWidth / window.innerHeight
  camera.updateProjectionMatrix()
  renderer.setSize(window.innerWidth, window.innerHeight)
}

onMounted(() => {
  initThree()
})

onUnmounted(() => {
  if (animationId) {
    cancelAnimationFrame(animationId)
  }
  window.removeEventListener('resize', onWindowResize)
  if (renderer) {
    renderer.dispose()
  }
})
</script>

<template>
  <div ref="containerRef" class="three-background"></div>
</template>

<style scoped>
.three-background {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: -1;
  pointer-events: none;
}

.three-background :deep(canvas) {
  width: 100% !important;
  height: 100% !important;
}
</style>
