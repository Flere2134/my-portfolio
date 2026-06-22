<template>
  <div class="portfolio-container">
    <header class="hero-section">
      <img src="./assets/img/profile-photo.jpg" alt="Aaron's Profile" class="profile-photo" />
      <div class="titles">
        <h1>Aaron</h1>
        <h2>Computer Engineer</h2>
        <div class="social-links">
          <a href="https://github.com/Flere2134" target="_blank" aria-label="GitHub">
            <svg viewBox="0 0 24 24" width="24" height="24" stroke="currentColor" stroke-width="2" fill="none" stroke-linecap="round" stroke-linejoin="round"><path d="M9 19c-5 1.5-5-2.5-7-3m14 6v-3.87a3.37 3.37 0 0 0-.94-2.61c3.14-.35 6.44-1.54 6.44-7A5.44 5.44 0 0 0 20 4.77 5.07 5.07 0 0 0 19.91 1S18.73.65 16 2.48a13.38 13.38 0 0 0-7 0C6.27.65 5.09 1 5.09 1A5.07 5.07 0 0 0 5 4.77a5.44 5.44 0 0 0-1.5 3.78c0 5.42 3.3 6.61 6.44 7A3.37 3.37 0 0 0 9 18.13V22"></path></svg>
          </a>
          <a href="https://linkedin.com/in/arboleda-aaron-hans-121b76372" target="_blank" aria-label="LinkedIn">
            <svg viewBox="0 0 24 24" width="24" height="24" stroke="currentColor" stroke-width="2" fill="none" stroke-linecap="round" stroke-linejoin="round"><path d="M16 8a6 6 0 0 1 6 6v7h-4v-7a2 2 0 0 0-2-2 2 2 0 0 0-2 2v7h-4v-7a6 6 0 0 1 6-6z"></path><rect x="2" y="9" width="4" height="12"></rect><circle cx="4" cy="4" r="2"></circle></svg>
          </a>
        </div>
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
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500&family=Montserrat:wght@700&display=swap');
/* Global Color Variables */
:root {
  --color-base: #0B4C53;
  --color-neutral: #F5F2E6 ;
  --color-accent: #C39B57;
}

body {
  margin: 0;
  font-family: 'Inter', system-ui, -apple-system, sans-serif;
  color: var(--color-base);
  
  /* The Gabardine Weave Effect */
  background-color: var(--color-neutral);
  background-image: repeating-linear-gradient(
    -45deg,
    transparent,
    transparent 2px,
    rgba(0, 103, 79, 0.03) 2px, /* Uses a tiny hint of your base green */
    rgba(0, 103, 79, 0.03) 4px
  );
}

.portfolio-container {
  min-height: 200vh;
}

/* Screen 1 Styles */
.hero-section {
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 60px; /* Increased gap for better breathing room */
  border-bottom: 4px solid var(--color-base);
}

.profile-circle {
  width: 200px;
  height: 200px;
  border-radius: 50%;
  border: 4px solid var(--color-base);
}

.profile-photo {
  width: 240px; /* Slightly larger for better impact */
  height: 240px;
  border-radius: 50%;
  object-fit: cover; /* Ensures your photo fills the circle without stretching */
  border: 4px solid var(--color-base);
  box-shadow: 0 12px 24px rgba(0, 103, 79, 0.15); /* Adds a refined, subtle shadow */
}

.titles {
  display: flex;
  flex-direction: column;
  gap: 8px; /* Tighter spacing between name and role */
}

.titles h1 {
  font-family: 'Montserrat', sans-serif;
  font-size: 5rem; /* Massive, striking name */
  font-weight: 700;
  margin: 0;
  letter-spacing: -1.5px; /* Pulls the letters slightly closer for a modern look */
  color: var(--color-base);
}

.titles h2 {
  font-family: 'Inter', sans-serif;
  font-size: 1.75rem;
  font-weight: 400;
  margin: 0;
  color: var(--color-accent); /* Using the plum color to make your role pop */
  letter-spacing: 1px;
}

.social-links {
  display: flex;
  gap: 16px;
  margin-top: 12px;
}

.social-links a {
  color: var(--color-base);
  transition: all 0.3s ease;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 8px;
  border-radius: 50%;
  background-color: rgba(0, 103, 79, 0.05); /* Subtle background circle */
}

.social-links a:hover {
  color: var(--color-accent);
  background-color: rgba(142, 69, 133, 0.1);
  transform: translateY(-2px); /* Slight lift on hover */
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