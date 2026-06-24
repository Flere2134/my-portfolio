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

    <div class="screen-2-bg">
      <main class="interactive-section">
        <InteractiveLever 
          :sections="portfolioSections" 
          @update:section="currentSection = $event" 
        />
        
        <section class="content-display">
          <transition name="reel" mode="out-in">
            <component :is="currentComponent" />
          </transition>
        </section>
      </main>
    </div>
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
  --color-bg-1: #07191C;    /* Midnight Peacock - For Screen 1 */
  --color-bg-2: #140D16;    /* Deep Velvet Plum - For Screen 2 Color Blocking */
  --color-text: #E8E6E1;    /* Crisp Off-White - Keeps text highly readable */
  --color-accent: #C39B57;  /* Casino Gold - Remains for our foil and accents */
  --color-cyan: #28C2C2;    /* Signature Turquoise - For subtle glowing effects */
}

body {
  margin: 0;
  font-family: 'Inter', system-ui, -apple-system, sans-serif;
  color: var(--color-text);
  background-color: var(--color-bg-1);
  
  /* The Dark Gabardine Weave Effect */
  background-image: repeating-linear-gradient(
    -45deg,
    transparent,
    transparent 2px,
    rgba(255, 255, 255, 0.02) 2px, 
    rgba(255, 255, 255, 0.02) 4px
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
  gap: 60px;
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
  background: linear-gradient(to right, #bf953f, #fcf6ba, #b38728, #fbf5b7, #aa771c);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  color: transparent;
}

.social-links {
  display: flex;
  gap: 16px;
  margin-top: 12px;
}

.social-links a {
  color: var(--color-text);
  transition: all 0.3s ease;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 8px;
  border-radius: 50%;
  background-color: rgba(255, 255, 255, 0.05);
}

.social-links a:hover {
  color: var(--color-cyan); /* They now glow signature turquoise on hover! */
  background-color: rgba(40, 194, 194, 0.1);
  transform: translateY(-2px); 
}

/* Dossier Button */
.dossier-btn {
  /* ... keep your existing properties, but update these: */
  color: var(--color-text);
}

.dossier-btn:hover {
  background-color: var(--color-accent);
  color: #000; /* Dark text on the gold background for high contrast */
  box-shadow: 0 0 20px rgba(195, 155, 87, 0.4); 
  transform: translateY(-2px);
}

/* Screen 2 Styles */
.screen-2-bg {
  background-color: var(--color-bg-2);
  width: 100%;
}

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
  background-color: rgba(255, 255, 255, 0.03); 
  border-radius: 12px;
  border: 1px solid rgba(195, 155, 87, 0.2); 
  box-shadow: 0 15px 35px rgba(0, 0, 0, 0.4); 
  
  position: relative; 
  overflow: hidden; 
}

.content-display h2 {
  color: var(--color-accent);
  margin-top: 0;
}

/* --- The Jackpot Reel Transition --- */
.reel-enter-active {
  /* The cubic-bezier adds that heavy mechanical 'thunk' and slight bounce at the end */
  transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.15); 
}

.reel-leave-active {
  /* The old content snaps away very quickly to simulate a fast spin */
  transition: all 0.15s ease-in; 
}

.reel-enter-from {
  opacity: 0;
  transform: translateY(-60px); /* Drops in from above */
  filter: blur(6px); /* Motion blur for high-speed effect */
}

.reel-leave-to {
  opacity: 0;
  transform: translateY(60px); /* Drops out below */
  filter: blur(6px);
}
</style>