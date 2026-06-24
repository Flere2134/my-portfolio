<template>
  <div class="lever-wrapper">
    <div class="reel-window">
      <div 
        class="reel-strip" 
        :style="{ transform: `translateY(-${activeIndex * 50}px)` }"
      >
        <div 
          v-for="(section, index) in sections" 
          :key="section"
          class="reel-item"
          :class="{ active: activeIndex === index }"
        >
          {{ section }}
          <span class="indicator-dot"></span>
        </div>
      </div>
    </div>
    
    <div class="track-casing">
      <div class="track" ref="trackRef">
        <div 
          class="handle" 
          :class="{ 'recoiling': !isDragging }"
          :style="{ transform: `translateY(${dragOffset}px)` }"
          @pointerdown="startDrag"
        >
          <div class="metal-rod"></div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import leverSoundUrl from '@/assets/audio/lever-clack.wav'
const leverAudio = new Audio(leverSoundUrl)
leverAudio.volume = 0.03

const props = defineProps({
  sections: {
    type: Array,
    required: true
  }
})

const emit = defineEmits(['update:section'])

const trackRef = ref(null)
const isDragging = ref(false)
const startY = ref(0)
const currentY = ref(0)
const activeIndex = ref(0)

// Maximum pixels the lever can be pulled in either direction
const maxDrag = 70 

// Calculates how far the lever is pulled from the center
const dragOffset = computed(() => {
  if (!isDragging.value) return 0 // Instantly snaps to 0 (center) when not dragging
  
  let offset = currentY.value - startY.value
  // Constrains the handle so it doesn't leave the track
  return Math.max(-maxDrag, Math.min(maxDrag, offset))
})

const startDrag = (event) => {
  isDragging.value = true
  startY.value = event.clientY
  currentY.value = event.clientY
  
  window.addEventListener('pointermove', onDrag)
  window.addEventListener('pointerup', stopDrag)
  event.preventDefault() 
}

const onDrag = (event) => {
  if (!isDragging.value) return
  currentY.value = event.clientY
}

const stopDrag = () => {
  const finalOffset = dragOffset.value
  const triggerThreshold = 35 
  
  if (finalOffset > triggerThreshold) {
    // Pulled DOWN -> Spin to the NEXT section
    if (activeIndex.value < props.sections.length - 1) {
      activeIndex.value++
      emit('update:section', props.sections[activeIndex.value])
    }
  } else if (finalOffset < -triggerThreshold) {
    // Pushed UP -> Spin to the PREVIOUS section
    if (activeIndex.value > 0) {
      activeIndex.value--
      emit('update:section', props.sections[activeIndex.value])
    }
  }

  // Play the mechanical snap sound!
  // We reset currentTime to 0 so the sound plays immediately even if they drag it rapidly
  leverAudio.currentTime = 0 
  leverAudio.play().catch(e => console.log("Audio play prevented by browser:", e))

  isDragging.value = false
  window.removeEventListener('pointermove', onDrag)
  window.removeEventListener('pointerup', stopDrag)
}
</script>

<style scoped>
.lever-wrapper {
  display: flex;
  align-items: center;
  gap: 30px;
  height: 240px;
}

/* --- The Slot Machine Reel System --- */
.reel-window {
  height: 150px; /* Shows 3 items at a time */
  width: 160px;
  position: relative;
  overflow: hidden;
  /* Fades out the top and bottom text to create a cylindrical illusion */
  -webkit-mask-image: linear-gradient(to bottom, transparent, black 25%, black 75%, transparent);
  mask-image: linear-gradient(to bottom, transparent, black 25%, black 75%, transparent);
}

.reel-strip {
  /* Pushes the first item down so it starts exactly in the center of the 150px window */
  padding-top: 50px; 
  /* The snappy, heavy spin animation */
  transition: transform 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.15); 
}

.reel-item {
  height: 50px; /* Precise height for mathematical transform offsets */
  display: flex;
  align-items: center;
  justify-content: flex-end;
  gap: 15px;
  font-family: 'Montserrat', sans-serif;
  text-transform: uppercase;
  font-weight: 700;
  letter-spacing: 2px;
  font-size: 0.9rem;
  color: var(--color-text);
  opacity: 0.2;
  transition: all 0.3s ease;
}

.reel-item.active {
  opacity: 1;
  color: var(--color-accent);
}

.indicator-dot {
  width: 6px;
  height: 6px;
  background-color: currentColor;
  border-radius: 50%;
  opacity: 0;
  transition: opacity 0.3s ease;
}

.reel-item.active .indicator-dot {
  opacity: 1;
}

/* --- The Mechanical Dark Casing --- */
.track-casing {
  padding: 10px 14px;
  background: linear-gradient(145deg, #1e1e1e, #0a0a0a);
  border-radius: 20px;
  box-shadow: 
    4px 4px 10px rgba(0, 0, 0, 0.6),
    -2px -2px 8px rgba(255, 255, 255, 0.05),
    inset 1px 1px 2px rgba(255, 255, 255, 0.05);
  border: 1px solid rgba(195, 155, 87, 0.15); 
  height: 180px; /* Fixed height so the lever has room to travel */
  display: flex;
  justify-content: center;
}

.track {
  width: 14px;
  background-color: #1a1a1a;
  border-radius: 8px;
  position: relative;
  box-shadow: 
    inset 0 4px 8px rgba(0,0,0,0.8),
    inset 0 1px 3px rgba(0,0,0,0.9);
  height: 100%;
}

/* --- The Spring-Loaded Handle --- */
.handle {
  width: 44px;
  height: 44px;
  background: radial-gradient(circle at 35% 35%, #ffbbee, var(--color-accent) 50%, #4a154b 90%);
  border-radius: 50%;
  
  /* Positions the handle absolutely in the dead center of the track */
  position: absolute;
  top: 50%; 
  left: 50%;
  margin-top: -22px; 
  margin-left: -22px; 
  
  cursor: grab;
  touch-action: none;
  box-shadow: 
    0 10px 15px rgba(0,0,0,0.3),
    0 4px 6px rgba(0,0,0,0.2),
    inset -4px -4px 8px rgba(0,0,0,0.3);
  z-index: 10;
}

.handle:active {
  cursor: grabbing;
  box-shadow: 
    0 5px 8px rgba(0,0,0,0.3),
    0 2px 4px rgba(0,0,0,0.2),
    inset -4px -4px 8px rgba(0,0,0,0.3);
}

/* When the user releases the mouse (!isDragging), this class is applied.
  It creates the violent, spring-loaded snap back to 0px (center). 
*/
.handle.recoiling {
  transition: transform 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
}

.metal-rod {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 60px;
  height: 12px;
  background: linear-gradient(to bottom, #bf953f, #fcf6ba 30%, #b38728 50%, #fbf5b7 70%, #aa771c);
  border-radius: 4px;
  z-index: -1;
  box-shadow: 0 4px 6px rgba(0,0,0,0.4);
}
</style>