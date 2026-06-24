<template>
  <div class="section-content">
    <h2>Experience</h2>
    
    <div class="experience-block">
      <h3>IT Support Intern</h3>
      <div class="date">Concentrix SM Megamall Branch | July – September 2025 | Mandaluyong</div>
      <ul>
        <li>Modernized a full production room's infrastructure, ensuring zero downtime during shifts, by executing mass hardware upgrades, software installations, and system cleanups</li>
        <li>Minimized technical disruptions for call center agents, resolving 50-60 tickets per week, by providing rapid troubleshooting and system diagostics.</li>
      </ul>
      <h3>Computer Technician Intern</h3>
      <div class="date">SDR Computer Trading| July – September 2024 | Quezon City</div>
      <ul>
        <li>Resolved hardware and software issues and malfunctions for an average of 5-10 customers per week, by performing systematic diagnostics and executing component repairs</li>
        <li>Assembled and deployed 25 complete desktop workstations for an educational institution in Palawan, by meticulously selecting and integrating compatible internal hardware components</li>
      </ul>
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
}

.experience-block h3 { 
  color: var(--color-text); 
  margin-bottom: 4px; 
  font-size: 1.3rem;
}

.date { 
  font-size: 0.9em; 
  color: var(--color-cyan); /* Pops nicely against the dark background */
  font-family: 'Montserrat', sans-serif;
  font-weight: 600;
  margin-bottom: 15px;
}

/* Custom Spades List */
ul { 
  list-style-type: none; 
  padding-left: 0;
  margin-top: 16px; 
}

li {
  position: relative;
  padding-left: 30px;
  margin-bottom: 14px;
  line-height: 1.7;
  color: #B0B0B0; /* Slightly dimmed text so the gold and cyan pop */
}

li::before {
  content: '\2660'; /* Gold Spade */
  position: absolute;
  left: 0;
  color: var(--color-accent);
  font-size: 1.3em;
  line-height: 1.4;
}
</style>