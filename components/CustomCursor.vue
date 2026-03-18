<template>
  <div class="cursor-container">
    <div ref="cursorDot" class="cursor-dot" :style="dotStyle"></div>
    <div class="cursor-ring" :style="dotStyle"></div>
    <canvas ref="canvas" class="cursor-canvas"></canvas>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted, reactive, computed } from 'vue';

const cursorDot = ref(null);
const canvas = ref(null);
const isHovering = ref(false);
let ctx = null;
let points = [];

const segments = 30;
const smoothness = 0.16;
const mouse = reactive({ x: -100, y: -100 });

const dotStyle = computed(() => ({
  transform: `translate3d(${mouse.x}px, ${mouse.y}px, 0) translate(-50%, -50%)`,
}));

const onMouseMove = (e) => {
  mouse.x = e.clientX;
  mouse.y = e.clientY;
};

const updateHover = (e) => {
  const target = e.target.closest('a, button, .btn-wrap');
  isHovering.value = !!target;
  document.body.classList.toggle('is-hovering', isHovering.value);
};

const animate = () => {
  if (!ctx || !canvas.value) return;
  ctx.clearRect(0, 0, canvas.value.width, canvas.value.height);

  let currX = mouse.x;
  let currY = mouse.y;

  points.forEach((point) => {
    point.x += (currX - point.x) * smoothness;
    point.y += (currY - point.y) * smoothness;
    currX = point.x;
    currY = point.y;
  });

  ctx.globalAlpha = isHovering.value ? 0.05 : 0.3;
  for (let i = 0; i < points.length - 1; i++) {
    const p1 = points[i];
    const p2 = points[i + 1];
    ctx.beginPath();
    ctx.moveTo(p1.x, p1.y);
    ctx.lineTo(p2.x, p2.y);
    const ratio = i / points.length;
    ctx.lineWidth = 1.5 * (1 - ratio);
    ctx.strokeStyle = '#e2d9c8';
    ctx.stroke();
  }
  requestAnimationFrame(animate);
};

const handleResize = () => {
  if (canvas.value) {
    canvas.value.width = window.innerWidth;
    canvas.value.height = window.innerHeight;
  }
};

onMounted(() => {
  ctx = canvas.value.getContext('2d');
  handleResize();
  for (let i = 0; i < segments; i++) points.push({ x: mouse.x, y: mouse.y });
  window.addEventListener('mousemove', onMouseMove);
  window.addEventListener('mouseover', updateHover);
  window.addEventListener('resize', handleResize);
  animate();
});

onUnmounted(() => {
  window.removeEventListener('mousemove', onMouseMove);
  window.removeEventListener('mouseover', updateHover);
  window.removeEventListener('resize', handleResize);
});
</script>

<style scoped>
.cursor-container {
  position: fixed;
  inset: 0;
  z-index: 10000;
  pointer-events: none;
}
.cursor-dot {
  position: absolute;
  width: 5px;
  height: 5px;
  background: #e2d9c8;
  border-radius: 50%;
  left: 0;
  top: 0;
  transition: opacity 0.3s ease;
}
.cursor-ring {
  position: absolute;
  width: 35px;
  height: 35px;
  border: 1px solid rgba(226, 217, 200, 0.2);
  border-radius: 50%;
  left: 0;
  top: 0;
  transition: width 0.5s cubic-bezier(0.19, 1, 0.22, 1),
    height 0.5s cubic-bezier(0.19, 1, 0.22, 1), background 0.3s ease;
}
:global(body.is-hovering) .cursor-ring {
  width: 70px;
  height: 70px;
  background: rgba(226, 217, 200, 0.1);
}
:global(body.is-hovering) .cursor-dot {
  opacity: 0;
}
.cursor-canvas {
  position: absolute;
  inset: 0;
  z-index: -1; /* Isay dot aur ring ke niche rakhein */
  pointer-events: none;
}
</style>
