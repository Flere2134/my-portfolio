<template>
  <div class="section-content">
    <h2>Experience & Research</h2>
    <div class="experience-block">
      <h3>Undergraduate Researcher</h3>
      <span class="date">Polytechnic University of the Philippines | 2025 – 2026</span>
      <ul>
        <li>Collaborated with a dedicated research group to design, prototype, and rigorously test hardware/software solutions.</li>
        <li>Managed data collection and established precise processing logic, including strict floor-rounding methodologies for accurate result interpretation.</li>
        <li>Successfully prepared and presented project manuscripts and prototypes for academic thesis defense panels.</li>
      </ul>
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

.experience-block h3 { 
  color: var(--color-base); 
  margin-bottom: 4px; 
}

.date { 
  font-size: 0.9em; 
  color: #666; 
  font-style: italic; 
}

/* Custom Card Suit List */
ul { 
  list-style-type: none; /* Removes the default dots */
  padding-left: 0;
  margin-top: 16px; 
}

li {
  position: relative;
  padding-left: 24px;
  margin-bottom: 12px;
  line-height: 1.6;
}

/* Inserts the Gold Spade */
li::before {
  content: '\2660'; /* Unicode for Spade */
  position: absolute;
  left: 0;
  color: var(--color-accent);
  font-size: 1.2em;
  line-height: 1.4; /* Aligns it nicely with the text */
}
</style>