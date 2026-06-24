<template>
  <div class="section-content">
    <h2>Projects</h2>

    <div class="projects-grid">
      <div class="project-card">
        <h3>Algorhythm: Smart Sleep Sound Therapy Device with Mobile Application</h3>
        <div class="tech-stack">Flutter / Figma / C++ / ESP32</div>
        <ul>
          <li>A sound therapy device that aims to improve sleep quality through sound therapy.</li>
          <li>Validated the device's effectiveness in improving sleep quality, successfully maintaining a 90% sleep efficiency rate, reducing sleep latency by 66%, through integration of ESP32 and dynamic fusion of sensors.</li>
          <li>Developed a functional sound therapy device, that has the ability to process ambient noise within milliseconds via digital audio amplifier.</li>
        </ul>
      </div>

      <div class="project-card">
        <h3>Echolocation Headgear</h3>
        <div class="tech-stack">C++ / Arduino Nano</div>
        <ul>
          <li>A wearable device designed to assist the visually impaired in navigating their environment.</li>
          <li>Engineered a prototype assistive echolocation wearable device, translating spatial proximity into real-time audio feedback for the visually challenged, by integrating to Arduino Nano with ultrasonic sensors.</li>
        </ul>
      </div>

      <div class="project-card">
        <h3>SaveSlot</h3>
        <div class="tech-stack">React / Vite / TypeScript / Supabase</div>
        <ul>
          <li>An interactive website where gamers can track games they played as well as share and rate their experiences with those games.</li>
        </ul>
      </div>

      <div class="project-card">
        <h3>GasGuard: Smart Gas Leak Detection System</h3>
        <div class="tech-stack">JavaScript / Vue / C++ / Firebase</div>
        <ul>
          <li>Developed a real-time gas leak detection system using IoT sensors and cloud-based analytics, ensuring seamless integration with various IoT protocols.</li>
          <li>Engineered a smart gas leak detection system, integrating sensors with real-time monitoring and alerts, by leveraging Firebase for data storage and Vue.js for the user interface.</li>
        </ul>
      </div>
    </div>
  </div>
</template>

<style scoped>
.section-content h2 { 
  color: var(--color-accent); 
  margin-top: 0; 
  font-family: 'Montserrat', sans-serif;
  letter-spacing: 2px;
  text-transform: uppercase;
  margin-bottom: 24px;
}

.projects-grid {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.project-card { 
  /* Deep VIP Dark Glass Effect */
  background: rgba(255, 255, 255, 0.02); 
  padding: 24px; 
  border-radius: 8px; 
  border-left: 4px solid var(--color-accent); 
  transition: transform 0.3s ease, background 0.3s ease;
}

.project-card:hover {
  background: rgba(255, 255, 255, 0.05);
  transform: translateX(5px);
}

.project-card h3 { 
  margin: 0 0 8px 0; 
  color: var(--color-text); 
  font-size: 1.2rem;
}

.tech-stack {
  font-size: 0.85em;
  color: var(--color-cyan);
  font-family: 'Montserrat', sans-serif;
  font-weight: 700;
  letter-spacing: 1px;
  margin-bottom: 16px;
}

/* Custom Clubs List */
ul { 
  list-style-type: none; 
  padding-left: 0;
  margin: 0;
}

li {
  position: relative;
  padding-left: 30px;
  margin-bottom: 10px;
  line-height: 1.6;
  color: #B0B0B0;
}

li::before {
  content: '\2663'; /* Gold Club */
  position: absolute;
  left: 0;
  color: var(--color-accent);
  font-size: 1.3em;
  line-height: 1.5;
}
</style>