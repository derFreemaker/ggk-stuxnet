<script setup lang="ts">
defineProps<{
  label?: string
}>()

import { vGlitch } from 'vue-powerglitch'

const glitch = {
  "timing": {
    "duration": 10000
  },
  "shake": {
    "velocity": 10,
    "amplitudeX": 0.2,
    "amplitudeY": 0.2,
  },
  "glitchTimeSpan": {
    "start": 0.2,
    "end": 0.3,
  }
}
</script>

<template>
  <div class="location-wrapper" v-glitch="glitch">
    <div class="location-content">
      <span v-if="label" class="label">{{ label }}</span>
      <div class="value">
        <slot />
      </div>
    </div>
  </div>
</template>

<style scoped>
.location-wrapper {
  position: relative;
  display: inline-flex;
  align-items: center;
  padding: 1rem 1.5rem;

  background:
    /* subtle scan lines */
    repeating-linear-gradient(
      to bottom,
      rgba(255,255,255,0.04) 0px,
      rgba(255,255,255,0.04) 1px,
      transparent 1px,
      transparent 3px
    ),
    linear-gradient(
      135deg,
      rgba(20, 22, 26, 0.95),
      rgba(32, 35, 40, 0.95)
    );

  border: 1px solid rgba(180, 180, 180, 0.25);
  border-radius: 0.5rem;
  font-family: "Courier New", monospace;
  letter-spacing: 0.08em;
  overflow: hidden;
  box-shadow: 0.15rem 0.4rem 5px 2px rgba(0, 0, 0, 0.75);

  position: fixed !important;
  top: 2rem;
  right: 2rem;
  z-index: 10;
}

.location-content {
  display: flex;
  gap: 1rem;
  align-items: center;
}

.label {
  font-size: 0.65rem;
  color: rgba(200, 200, 200, 0.5);
  text-transform: uppercase;
}

.value {
  font-size: 1rem;
  color: #e6e6e6;
  display: flex;
  align-items: center;
  gap: 0.6rem;
}
</style>
