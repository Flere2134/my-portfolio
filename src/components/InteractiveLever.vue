<template>
  <div class="lever-wrapper">
    <div class="labels">
      <div 
        v-for="(section, index) in sections" 
        :key="section"
        class="label"
        :class="{ active: activeIndex === index }"
      >
        {{ section }}
        <span class="indicator-dot"></span>
      </div>
    </div>
    
    <div class="track-casing">
      <div class="track" ref="trackRef">
        <div 
          class="handle" 
          :class="{ 'recoiling': isRecoiling }"
          :style="{ transform: `translateY(${handleY}px)` }"
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

const props = defineProps({
  sections: {
    type: Array,
    required: true
  }
})

const emit = defineEmits(['update:section'])

const trackRef = ref(null)
const handleY = ref(0)
const activeIndex = ref(0)
const isDragging = ref(false)
const isRecoiling = ref(false)

const startDrag = (event) => {
  isDragging.value = true
  window.addEventListener('pointermove', onDrag)
  window.addEventListener('pointerup', stopDrag)
  // Prevent default scrolling while dragging on touch devices
  event.preventDefault() 
}

const onDrag = (event) => {
  if (!isDragging.value || !trackRef.value) return

  const trackRect = trackRef.value.getBoundingClientRect()
  
  // Calculate relative Y position within the track boundaries
  let newY = event.clientY - trackRect.top
  
  // Constrain the handle within the track (0 to track height)
  newY = Math.max(0, Math.min(newY, trackRect.height))
  handleY.value = newY

  // Calculate progress ratio (0.0 to 1.0)
  const progress = newY / trackRect.height
  
  // Determine which section we are in.
  // We strictly floor the value to ensure it maps correctly to our array indices [0, 1, 2, 3]
  let mappedIndex = Math.floor(progress * props.sections.length)
  
  // Edge case: if dragged to the absolute bottom edge, cap it at the last index
  if (mappedIndex >= props.sections.length) {
    mappedIndex = props.sections.length - 1
  }

  if (activeIndex.value !== mappedIndex) {
    activeIndex.value = mappedIndex
    emit('update:section', props.sections[mappedIndex])
  }
}

const stopDrag = () => {
  isDragging.value = false
  
  // Trigger the mechanical recoil animation
  isRecoiling.value = true
  setTimeout(() => {
    isRecoiling.value = false
  }, 250) // The timeout matches the CSS animation duration

  window.removeEventListener('pointermove', onDrag)
  window.removeEventListener('pointerup', stopDrag)
}
</script>

<style scoped>
.lever-wrapper {
  display: flex;
  align-items: stretch;
  gap: 30px;
  height: 320px;
  padding: 20px 0;
}

/* Typography and Labels */
.labels {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  text-align: right;
  font-weight: bold;
  color: var(--color-base);
  font-family: 'Montserrat', sans-serif;
  text-transform: uppercase;
  letter-spacing: 2px;
  font-size: 0.9rem;
  padding: 10px 0;
}

.label {
  opacity: 0.3;
  transition: all 0.3s ease;
  position: relative;
  display: flex;
  align-items: center;
  justify-content: flex-end;
  gap: 15px;
}

.label.active {
  opacity: 1;
  color: var(--color-accent);
  transform: translateX(5px);
}

.indicator-dot {
  width: 6px;
  height: 6px;
  background-color: currentColor;
  border-radius: 50%;
  opacity: 0;
  transition: opacity 0.3s ease;
}

.label.active .indicator-dot {
  opacity: 1;
}

/* The Dark Mechanical Casing */
.track-casing {
  padding: 10px 14px;
  /* Dark brushed metal gradient */
  background: linear-gradient(145deg, #1e1e1e, #0a0a0a);
  border-radius: 20px;
  box-shadow: 
    4px 4px 10px rgba(0, 0, 0, 0.6),
    -2px -2px 8px rgba(255, 255, 255, 0.05),
    inset 1px 1px 2px rgba(255, 255, 255, 0.05);
  border: 1px solid rgba(195, 155, 87, 0.15); /* Faint gold rim */
  display: flex;
  justify-content: center;
}

/* The Recessed Slot */
.track {
  width: 14px;
  background-color: #1a1a1a;
  border-radius: 8px;
  position: relative;
  cursor: pointer;
  /* Creates the deep groove effect */
  box-shadow: 
    inset 0 4px 8px rgba(0,0,0,0.8),
    inset 0 1px 3px rgba(0,0,0,0.9);
}

/* The Glossy Sphere Knob */
.handle {
  width: 44px;
  height: 44px;
  /* 3D Radial Gradient to make it look like a polished gem or casino chip */
  background: radial-gradient(circle at 35% 35%, #ffbbee, var(--color-accent) 50%, #4a154b 90%);
  border-radius: 50%;
  position: absolute;
  top: -22px; 
  left: -15px; 
  cursor: grab;
  touch-action: none;
  /* Heavy drop shadow so it hovers above the track */
  box-shadow: 
    0 10px 15px rgba(0,0,0,0.3),
    0 4px 6px rgba(0,0,0,0.2),
    inset -4px -4px 8px rgba(0,0,0,0.3);
  transition: transform 0.05s linear;
  z-index: 10;
}

.handle:active {
  cursor: grabbing;
  /* Compress the shadow slightly to simulate pressing down */
  box-shadow: 
    0 5px 8px rgba(0,0,0,0.3),
    0 2px 4px rgba(0,0,0,0.2),
    inset -4px -4px 8px rgba(0,0,0,0.3);
}

/* The Gold Metal Arm */
.metal-rod {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 60px;
  height: 12px;
  /* Brushed gold effect */
  background: linear-gradient(to bottom, #bf953f, #fcf6ba 30%, #b38728 50%, #fbf5b7 70%, #aa771c);
  border-radius: 4px;
  z-index: -1;
  box-shadow: 0 4px 6px rgba(0,0,0,0.4);
}

/* The Mechanical Recoil Animation */
.handle.recoiling {
  /* Using a custom bezier curve for a snappy, spring-like feel */
  animation: mechanical-recoil 0.25s cubic-bezier(0.36, 0.07, 0.19, 0.97) both;
}

@keyframes mechanical-recoil {
  0% { margin-top: 0; }
  35% { margin-top: 6px; }  /* Heavy drop when released */
  65% { margin-top: -2px; } /* Slight bounce back up */
  100% { margin-top: 0; }   /* Settles into the locked position */
}
</style>