<template>
  <div class="portfolio-container">
    <header class="hero-section">
      <div class="profile-circle"></div>
      <div class="titles">
        <h1>Aaron</h1>
        <h2>Computer Engineer</h2>
      </div>
    </header>

    <main class="interactive-section">
      <InteractiveLever 
        :sections="portfolioSections" 
        @update:section="currentSection = $event" 
      />
      
      <section class="content-display">
        <transition name="fade" mode="out-in">
          <component :is="currentComponent" />
        </transition>
      </section>
    </main>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import InteractiveLever from './components/InteractiveLever.vue'

// Import your actual content components
import AboutMe from './components/AboutMe.vue'
import Experience from './components/Experience.vue'
import Projects from './components/Projects.vue'
import Skills from './components/Skills.vue'

// Map the section names to the imported files
const componentMap = {
  'About Me': AboutMe,
  'Experience': Experience,
  'Projects': Projects,
  'Skills': Skills
}

const portfolioSections = Object.keys(componentMap)
const currentSection = ref(portfolioSections[0])

// This computed property automatically figures out which component to show
const currentComponent = computed(() => componentMap[currentSection.value])
</script>

<style>
/* Global Color Variables */
:root {
  --color-base: #00674F;
  --color-neutral: #FDFBD4;
  --color-accent: #8E4585;
}

body {
  margin: 0;
  font-family: system-ui, -apple-system, sans-serif;
  background-color: var(--color-neutral);
  color: var(--color-base);
}

.portfolio-container {
  min-height: 200vh; /* Forces the page to be scrollable past Screen 1 */
}

/* Screen 1 Styles */
.hero-section {
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 40px;
  border-bottom: 4px solid var(--color-base);
}

.profile-circle {
  width: 200px;
  height: 200px;
  border-radius: 50%;
  border: 4px solid var(--color-base);
}

/* Screen 2 Styles */
.interactive-section {
  min-height: 100vh;
  padding: 100px 50px;
  display: flex;
  align-items: center;
  gap: 80px;
  max-width: 1200px;
  margin: 0 auto;
}

.content-display {
  flex: 1;
  padding: 40px;
  background-color: white;
  border-radius: 12px;
  box-shadow: 0 10px 30px rgba(0, 103, 79, 0.1);
}

.content-display h2 {
  color: var(--color-accent);
  margin-top: 0;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.15s ease;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>