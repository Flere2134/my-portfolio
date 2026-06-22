<template>
  <div class="section-content">
    <h2>Featured Projects</h2>
    
    <div class="project-card">
      <h3>Smart Sleep Therapy System</h3>
      <p>An integrated IoT ecosystem designed to provide sound therapy.</p>
      <ul>
        <li><strong>Hardware:</strong> Engineered using ESP32/ESP8266 microcontrollers and integrated I2S radar modules/sensors housed in custom 3D-printed PLA/PETG enclosures.</li>
        <li><strong>Software:</strong> Developed the companion mobile application utilizing Vue and Nuxt for a reactive, user-friendly interface.</li>
      </ul>
    </div>

    <div class="project-card">
      <h3>2D Logic Board Game</h3>
      <p>A custom game project developed in Godot 4.6.</p>
      <ul>
        <li>Implemented core mechanics blending Snakes & Ladders with Rock-Paper-Scissors rulesets.</li>
        <li>Engineered 2D board state logic, viewport management, and dynamic player interactions.</li>
      </ul>
    </div>
  </div>
</template>

<style scoped>
.section-content h2 { color: var(--color-accent); margin-top: 0; }
.project-card { 
  background: rgba(0, 103, 79, 0.05); 
  padding: 20px; 
  border-radius: 8px; 
  margin-bottom: 20px;
  border-left: 4px solid var(--color-base);
}
.project-card h3 { margin-top: 0; color: var(--color-base); }
</style>