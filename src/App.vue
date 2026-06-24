<template>
  <div class="portfolio-container">
    <header class="hero-section">
      <div 
        class="scenic-overlay" 
        :style="{ backgroundImage: `url(${scenicBgUrl})` }"
      ></div>
      <div class="hero-container">
        <div class="left-content">
          <div class="titles">
            <h1>This is Aaron</h1>
            <h2>Computer Engineer</h2>
          </div>
          
          <div class="social-links">
            <a href="https://github.com/yourusername" target="_blank" aria-label="GitHub">
              <svg viewBox="0 0 24 24" width="24" height="24" stroke="currentColor" stroke-width="2" fill="none" stroke-linecap="round" stroke-linejoin="round"><path d="M9 19c-5 1.5-5-2.5-7-3m14 6v-3.87a3.37 3.37 0 0 0-.94-2.61c3.14-.35 6.44-1.54 6.44-7A5.44 5.44 0 0 0 20 4.77 5.07 5.07 0 0 0 19.91 1S18.73.65 16 2.48a13.38 13.38 0 0 0-7 0C6.27.65 5.09 1 5.09 1A5.07 5.07 0 0 0 5 4.77a5.44 5.44 0 0 0-1.5 3.78c0 5.42 3.3 6.61 6.44 7A3.37 3.37 0 0 0 9 18.13V22"></path></svg>
            </a>
            <a href="https://linkedin.com/in/yourusername" target="_blank" aria-label="LinkedIn">
              <svg viewBox="0 0 24 24" width="24" height="24" stroke="currentColor" stroke-width="2" fill="none" stroke-linecap="round" stroke-linejoin="round"><path d="M16 8a6 6 0 0 1 6 6v7h-4v-7a2 2 0 0 0-2-2 2 2 0 0 0-2 2v7h-4v-7a6 6 0 0 1 6-6z"></path><rect x="2" y="9" width="4" height="12"></rect><circle cx="4" cy="4" r="2"></circle></svg>
            </a>
          </div>

          <a href="/resume.pdf" class="dossier-btn prominent" target="_blank">GET THE DOSSIER</a>
        </div>
        
        <div class="right-content">
          <img src="./assets/img/profile-photo.jpg" alt="Aaron's Profile" class="profile-photo massive" />
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
import AboutMe from './components/AboutMe.vue'
import Experience from './components/Experience.vue'
import Projects from './components/Projects.vue'
import Skills from './components/Skills.vue'
import scenicBgUrl from '@/assets/img/scenic-background.jpg'

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
  gap: 100px; 
  position: relative;
  background-color: var(--color-bg-1);
  overflow: hidden; /* Keeps the image contained */
}

/* The new scenic overlay class */
.scenic-overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-size: cover;
  background-position: center;
  opacity: 0.85; /* Keep it subtle */
  z-index: 0;
}

/* Ensure the dark green base color is applied over the image */
.hero-section::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(7, 25, 28, 0.85); /* Midnight peacock */
  z-index: 1;
}

.hero-container {
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 100%;
  max-width: 1400px; /* Constrains the maximum width */
  padding: 0 80px; /* Pulls content away from the edges */
  z-index: 2; /* Ensures it sits above the background */
}

/* All content within the hero sits above the overlays */
.left-content,
.right-content {
  z-index: 2;
  flex: 1; /* Both sides share space equally */
}

.left-content {
  display: flex;
  flex-direction: column;
  align-items: flex-start; /* Sharp left alignment */
  gap: 24px;
  flex: 0 1 auto;
}

/* 3. Massive Typography for Name and Role */
.titles h1 {
  font-family: 'Montserrat', sans-serif;
  font-size: 6.5rem; /* Massive, commanding name */
  font-weight: 700;
  margin: 0;
  letter-spacing: -2px; /* Pulls the large letters tighter for a modern look */
  color: var(--color-text);
}

.titles h2 {
  font-family: 'Inter', sans-serif;
  font-size: 2.2rem; /* Much larger and bolder role text */
  font-weight: 400;
  margin: 0;
  letter-spacing: 1px;
  
  /* Scaled up the original Brushed Gold Foil Effect */
  background: linear-gradient(to right, #bf953f, #fcf6ba, #b38728, #fbf5b7, #aa771c);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  color: transparent; /* Fallback */
}

.right-content {
  display: flex;
  justify-content: flex-end;
  align-items: center;
  flex: 0 1 auto;
}

/* 4. Dramatically Massive Profile Photo with Refined Glow */
.profile-photo.massive {
  width: 440px; /* Dramatic scale */
  height: 440px;
  border-radius: 50%;
  object-fit: cover;
  /* Remove the simple border and add a refined glow to make it stand out */
  border: none;
  box-shadow: 0 15px 40px rgba(0, 0, 0, 0.5), 0 0 50px rgba(40, 194, 194, 0.15); /* Adds presence and a subtle cyan hint */
}

/* Adjust social icons for left alignment and better flow */
.social-links {
  display: flex;
  gap: 20px;
  margin-top: 10px;
  margin-bottom: 10px;
  align-self: flex-start; /* Force left alignment */
}

.social-links a {
  color: var(--color-text);
  background-color: rgba(255, 255, 255, 0.05);
  box-shadow: inset 0 1px 1px rgba(255,255,255,0.05);
}

.social-links a:hover {
  color: var(--color-cyan);
  background-color: rgba(40, 194, 194, 0.1);
  transform: translateY(-2px) scale(1.05); /* Adds a slight lift and scale on hover */
}

/* Bolder, More Prominent Dossier Button */
.dossier-btn.prominent {
  margin-top: 0; 
  padding: 16px 40px; 
  border: 3px solid var(--color-accent); /* Casino Gold border */
  border-radius: 50px;
  
  /* FIX: Force the text to be your crisp off-white and remove default underlines */
  color: var(--color-text); 
  text-decoration: none; 
  
  /* Make it heavily bolded to match the reference */
  font-family: 'Montserrat', sans-serif;
  font-weight: 800; /* Extra bold */
  font-size: 1.1rem; 
  letter-spacing: 3px; 
  align-self: flex-start; 
  transition: all 0.3s ease;
}

.dossier-btn.prominent:hover {
  /* Fills with that beautiful gold/light brown on hover */
  background-color: var(--color-accent);
  
  /* Text turns to your deep dark background color for high contrast */
  color: var(--color-bg-1); 
  
  box-shadow: 0 0 30px rgba(195, 155, 87, 0.4); 
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