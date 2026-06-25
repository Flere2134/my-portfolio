<template>
  <canvas ref="canvasRef" class="ambient-canvas"></canvas>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const canvasRef = ref(null)
let animationFrameId = null

// Your Locked Parameters
const PARTICLE_COUNT = 108
const BASE_SPEED = 1.5
const BASE_SIZE = 2.5
const MAX_OPACITY = 0.6

// VIP Theme: Casino Gold and Signature Turquoise
const colors = ['195, 155, 87', '40, 194, 194']

onMounted(() => {
  const canvas = canvasRef.value
  const ctx = canvas.getContext('2d')
  let particles = []

  // Ensures the canvas always fits the exact size of the screen
  const resize = () => {
    canvas.width = window.innerWidth
    canvas.height = window.innerHeight
  }

  window.addEventListener('resize', resize)
  resize()

  class Particle {
    constructor() {
      this.x = Math.random() * canvas.width
      this.y = Math.random() * canvas.height
      // Calculates a slow, steady drift based on your Speed parameter
      this.vx = (Math.random() - 0.5) * BASE_SPEED
      this.vy = (Math.random() - 0.5) * BASE_SPEED
      this.size = Math.random() * BASE_SIZE + 1
      this.color = colors[Math.floor(Math.random() * colors.length)]
      
      this.opacity = Math.random() * MAX_OPACITY
      this.fadeDir = Math.random() > 0.5 ? 0.005 : -0.005
    }

    update() {
      this.x += this.vx
      this.y += this.vy

      // Seamlessly wraps the particles around the screen edges
      if (this.x < 0) this.x = canvas.width
      if (this.x > canvas.width) this.x = 0
      if (this.y < 0) this.y = canvas.height
      if (this.y > canvas.height) this.y = 0

      // Creates the slow, ambient pulse effect
      this.opacity += this.fadeDir
      if (this.opacity >= MAX_OPACITY || this.opacity <= 0.1) {
        this.fadeDir *= -1
      }
    }

    draw() {
      ctx.beginPath()
      ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2)
      ctx.fillStyle = `rgba(${this.color}, ${this.opacity})`
      ctx.fill()
    }
  }

  // Populate the array with your 60 particles
  for (let i = 0; i < PARTICLE_COUNT; i++) {
    particles.push(new Particle())
  }

  // The continuous 60fps render loop
  const animate = () => {
    ctx.clearRect(0, 0, canvas.width, canvas.height)
    particles.forEach(p => {
      p.update()
      p.draw()
    })
    animationFrameId = requestAnimationFrame(animate)
  }

  animate()
})

onUnmounted(() => {
  window.removeEventListener('resize', resize)
  cancelAnimationFrame(animationFrameId)
})
</script>

<style scoped>
.ambient-canvas {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  pointer-events: none; 
  z-index: 3; 
}
</style>