<template>
  <div class="app-container">
    <CustomCursor />

    <div class="stone-bg">
      <div class="spotlight"></div>
    </div>

    <slot />
  </div>
</template>

<script setup>
import { onMounted, onUnmounted } from 'vue';

// Mouse position track karna zaroori hai spotlight ke liye
const updateMousePos = (e) => {
  document.documentElement.style.setProperty('--x', `${e.clientX}px`);
  document.documentElement.style.setProperty('--y', `${e.clientY}px`);
};

onMounted(() => {
  window.addEventListener('mousemove', updateMousePos);
});

onUnmounted(() => {
  window.removeEventListener('mousemove', updateMousePos);
});
</script>

<style>
/* Global Styles jo puri website par chalenge */
:root {
  --c-yellow: #e2d9c8;
  --f-cubic: cubic-bezier(0.35, 0.35, 0, 1);
  --x: 0px;
  --y: 0px;
}

body {
  margin: 0;
  background-color: #151415;
  overflow-x: hidden;
  /* Original cursor hide karna mat bhooliyega */
  cursor: none;
}

/* Background aur Spotlight ki settings */
.stone-bg {
  position: fixed;
  inset: 0;
  z-index: -1;
  background: #1a191a;
  background-image: radial-gradient(#222 1px, transparent 0);
  background-size: 4px 4px;
}

.spotlight {
  position: absolute;
  inset: 0;
  background: radial-gradient(
    600px circle at var(--x) var(--y),
    rgba(255, 255, 255, 0.04) 0%,
    transparent 100%
  );
  pointer-events: none;
}
</style>
