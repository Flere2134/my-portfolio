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
      </div>
    </div>
    
    <div class="track" ref="trackRef">
      <div 
        class="handle" 
        :style="{ transform: `translateY(${handleY}px)` }"
        @pointerdown="startDrag"
      ></div>
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
  window.removeEventListener('pointermove', onDrag)
  window.removeEventListener('pointerup', stopDrag)
}
</script>

<style scoped>
.lever-wrapper {
  display: flex;
  align-items: stretch;
  gap: 20px;
  height: 300px;
}

.labels {
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  text-align: right;
  font-weight: bold;
  color: var(--color-base);
}

.label {
  opacity: 0.5;
  transition: opacity 0.3s ease;
}

.label.active {
  opacity: 1;
  color: var(--color-accent);
}

.track {
  width: 8px;
  background-color: var(--color-base);
  border-radius: 4px;
  position: relative;
  cursor: pointer;
}

.handle {
  width: 24px;
  height: 24px;
  background-color: var(--color-accent);
  border-radius: 50%;
  position: absolute;
  top: -12px; /* Center the handle on the 0 position */
  left: -8px; /* Center horizontally over the track */
  cursor: grab;
  touch-action: none;
  box-shadow: 0 4px 6px rgba(0,0,0,0.3);
  transition: transform 0.05s linear;
}

.handle:active {
  cursor: grabbing;
}
</style>