<template>
  <div class="section-content">
    <h2>Technical Skills</h2>
    <div class="skills-grid">
      <div class="skill-category">
        <h3>Hardware & Embedded</h3>
        <ul>
          <li>ESP32 & ESP8266 Development</li>
          <li>Sensor Integration (I2S, Radar)</li>
          <li>Circuit Prototyping (Buck Converters, IoT)</li>
          <li>3D Printing (PLA, PETG)</li>
        </ul>
      </div>
      <div class="skill-category">
        <h3>Software & Web</h3>
        <ul>
          <li>Vue.js & Nuxt.js</li>
          <li>JavaScript (ES6+)</li>
          <li>C++ (Arduino Framework)</li>
          <li>Godot Engine (GDScript)</li>
          <li>Git & GitHub Actions (CI/CD)</li>
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
  letter-spacing: 1px;
}

.skills-grid { 
  display: flex; 
  gap: 40px; 
}

.skill-category h3 { 
  color: var(--color-base); 
  border-bottom: 2px solid var(--color-accent); /* Changed to gold for a richer look */
  padding-bottom: 8px;
}

/* Custom Card Suit List */
ul { 
  list-style-type: none; 
  padding-left: 0;
}

li {
  position: relative;
  padding-left: 20px;
  margin-bottom: 10px;
  line-height: 1.8;
}

/* Inserts the Gold Diamond */
li::before {
  content: '\2666'; /* Unicode for Diamond */
  position: absolute;
  left: 0;
  color: var(--color-accent);
  font-size: 1.1em;
  line-height: 1.6;
}
</style>