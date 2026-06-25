<template>
  <div class="section-content">
    <h2>Experience Archive</h2>
    
    <div class="slot-machine-casing">
      <div class="reels-container">
        
        <div class="reel-window" v-for="(reel, reelIndex) in 3" :key="reelIndex">
          <div class="reel-strip" :class="`spin-speed-${reelIndex}`">
            <div class="image-slot" v-for="(img, imgIndex) in imageStrip" :key="imgIndex">
              <img :src="img.src" alt="Internship Memory" />
            </div>
          </div>
        </div>
        
      </div>
    </div>
  </div>
</template>

<script setup>
// We no longer need Vue 'ref' state because pure CSS handles the ambient rolling
import img1 from '@/assets/img/exp-1.jpg'
import img2 from '@/assets/img/exp-2.jpg'
import img3 from '@/assets/img/exp-3.jpg'
import img4 from '@/assets/img/exp-4.jpg'
import img5 from '@/assets/img/exp-5.jpg'
import img6 from '@/assets/img/exp-6.jpg'


// Your unique images
const baseImages = [
  { src: img1 },
  { src: img2 },
  { src: img3 },
  { src: img4 },
  { src: img5 },
  { src: img6 }
]

const imageStrip = [...baseImages, ...baseImages]
</script>

<style scoped>
.section-content {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.section-content h2 { 
  color: var(--color-accent); 
  font-family: 'Montserrat', sans-serif;
  letter-spacing: 2px;
  text-transform: uppercase;
  margin-bottom: 40px;
}

/* The Dark VIP Machine Casing */
.slot-machine-casing {
  background: linear-gradient(145deg, #140d16, #0a0a0a);
  padding: 40px; /* Slightly more padding for the larger scale */
  border-radius: 16px;
  border: 2px solid rgba(195, 155, 87, 0.3);
  box-shadow: 
    0 20px 40px rgba(0, 0, 0, 0.8),
    inset 0 0 20px rgba(0,0,0,0.5);
  margin-bottom: 40px;
  width: 100%;
  max-width: 1350px; 
  display: flex;
  justify-content: center;
}

.reels-container {
  display: flex;
  gap: 30px; 
  box-shadow: inset 0 10px 20px rgba(0,0,0,0.8), inset 0 -10px 20px rgba(0,0,0,0.8);
  border-radius: 8px;
  padding: 20px;
  background-color: #050505;
}

/* Scaled up Reel Windows */
.reel-window {
  width: 400px;
  height: 400px;
  overflow: hidden;
  position: relative;
  border-radius: 4px;
  border: 1px solid rgba(255, 255, 255, 0.05);
}

.reel-strip {
  display: flex;
  flex-direction: column;
  width: 100%;
}

.spin-speed-0 {
  animation: scroll-ambient 32s linear infinite;
}

.spin-speed-1 {
  animation: scroll-ambient 26s linear infinite;
}

.spin-speed-2 {
  animation: scroll-ambient 29s linear infinite;
}

@keyframes scroll-ambient {
  0% { transform: translateY(0); }
  100% { transform: translateY(-50%); }
}

/* Pauses the animation if a recruiter hovers their mouse to look closely at a specific photo */
.reel-window:hover .reel-strip {
  animation-play-state: paused;
}

/* Scaled up Image Slots */
.image-slot {
  width: 400px;
  height: 400px;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 15px;
  box-sizing: border-box;
  flex-shrink: 0;
}

.image-slot img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 4px;
  box-shadow: 0 4px 10px rgba(0,0,0,0.5);
  filter: brightness(0.7) contrast(1.1);
  transition: filter 0.4s ease;
}

.image-slot:hover img {
  filter: brightness(1) contrast(1);
}

@media (max-width: 1024px) {
  .slot-machine-casing {
    padding: 20px 15px; 
    border-radius: 12px;
  }

  .reels-container {
    gap: 10px; 
    padding: 10px;
  }

  .reel-window {
    width: 28vw; 
    height: 28vw;
    max-width: 250px;
    max-height: 250px;
  }

  .image-slot {
    width: 100%;
    height: 100%;
    padding: 5px;
  }
  
  .section-content h2 {
    font-size: 1.5rem; 
    margin-bottom: 25px;
    text-align: center;
  }
}
</style>