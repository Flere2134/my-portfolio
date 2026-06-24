<template>
  <div class="section-content">
    <h2>Technical Arsenal</h2>
    
    <div class="skills-grid">
      <div class="skill-category">
        <h3>Hardware & IoT</h3>
        <ul>
          <li>ESP32 Microcontrollers</li>
          <li>Sensor Integration (I2S Microphones, Radar Modules)</li>
          <li>Embedded Systems Architecture</li>
          <li>PC Assembly & Troubleshooting</li>
        </ul>
      </div>

      <div class="skill-category">
        <h3>Languages & Frameworks</h3>
        <ul>
          <li>C++</li>
          <li>Vue.js & Nuxt.js (Reactive Front-end)</li>
          <li>Firebase</li>
          <li>Flutter & Dart</li>
          <li>MySQL</li>
          <li>HTML & CSS</li>
          <li>JavaScript</li>
        </ul>
      </div>

      <div class="skill-category">
        <h3>Soft Skills</h3>
        <ul>
          <li>Adaptability</li>
          <li>Resourcefulness</li>
          <li>Technical Translation</li>
          <li>Technical Writing</li>
          <li>Cross-Functional Collaboration</li>
          <li>Receptive to Feedback</li>
          <li>Time Management</li>
          <li>Initiative</li>
          <li>User-Centric Design</li>
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
  margin-bottom: 32px;
}

.skills-grid { 
  display: grid; 
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 30px; 
}

.skill-category {
  /* VIP Dark Glass Effect matches the Projects section */
  background: rgba(255, 255, 255, 0.02); 
  padding: 24px; 
  border-radius: 8px; 
  border-top: 3px solid var(--color-cyan); /* Signature Turquoise top border */
  transition: transform 0.3s ease, background 0.3s ease;
}

.skill-category:hover {
  background: rgba(255, 255, 255, 0.04);
  transform: translateY(-4px);
}

.skill-category h3 { 
  color: var(--color-text); 
  margin-top: 0;
  margin-bottom: 16px;
  padding-bottom: 12px;
  border-bottom: 1px solid rgba(195, 155, 87, 0.2); /* Faint gold divider */
  font-size: 1.15rem;
  letter-spacing: 1px;
}

/* Custom Diamond List */
ul { 
  list-style-type: none; 
  padding-left: 0;
  margin: 0;
}

li {
  position: relative;
  padding-left: 28px;
  margin-bottom: 12px;
  line-height: 1.5;
  color: #B0B0B0;
  font-size: 0.95rem;
}

/* Inserts the Gold Diamond */
li::before {
  content: '\2666'; /* Unicode for Diamond */
  position: absolute;
  left: 0;
  top: 1px;
  color: var(--color-accent);
  font-size: 1.1em;
}
</style>