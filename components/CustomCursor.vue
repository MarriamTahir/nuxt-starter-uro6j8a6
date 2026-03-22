<template>
  <div class="cursor-container">
    <div class="cursor-dot" :style="cursorStyle"></div>
    <div class="cursor-ring" :class="{ 'is-active': isHovering }" :style="cursorStyle"></div>
    <canvas ref="canvas" class="cursor-canvas"></canvas>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted, reactive, computed } from 'vue';

const canvas = ref(null);
const isHovering = ref(false);
const mouse = reactive({ x: -100, y: -100 });
let ctx = null;
let points = [];
const segments = 25;

const cursorStyle = computed(() => ({
  transform: `translate3d(${mouse.x}px, ${mouse.y}px, 0) translate(-50%, -50%)`
}));

const onMouseMove = (e) => {
  mouse.x = e.clientX;
  mouse.y = e.clientY;
};

const updateHover = (e) => {
  // .interactive class check karega
  isHovering.value = !!e.target.closest('a, button, .interactive');
};

const animate = () => {
  if (!ctx || !canvas.value) return;
  ctx.clearRect(0, 0, canvas.value.width, canvas.value.height);
  let currX = mouse.x;
  let currY = mouse.y;

  points.forEach((p) => {
    p.x += (currX - p.x) * 0.15;
    p.y += (currY - p.y) * 0.15;
    currX = p.x; currY = p.y;
  });

  ctx.globalAlpha = isHovering.value ? 0.05 : 0.2;
  for (let i = 0; i < points.length - 1; i++) {
    ctx.beginPath();
    ctx.moveTo(points[i].x, points[i].y);
    ctx.lineTo(points[i+1].x, points[i+1].y);
    ctx.lineWidth = 1.2 * (1 - i/points.length);
    ctx.strokeStyle = '#e2d9c8';
    ctx.stroke();
  }
  requestAnimationFrame(animate);
};

onMounted(() => {
  ctx = canvas.value.getContext('2d');
  canvas.value.width = window.innerWidth;
  canvas.value.height = window.innerHeight;
  for (let i = 0; i < segments; i++) points.push({ x: mouse.x, y: mouse.y });
  window.addEventListener('mousemove', onMouseMove);
  window.addEventListener('mouseover', updateHover);
  animate();
});
</script>

<style scoped>
.cursor-container { position: fixed; inset: 0; z-index: 10000; pointer-events: none; }
.cursor-dot {
  position: absolute; width: 4px; height: 4px; background: #e2d9c8;
  border-radius: 50%; left: 0; top: 0;
}
.cursor-ring {
  position: absolute; width: 30px; height: 30px;
  border: 1px solid rgba(226, 217, 200, 0.3);
  border-radius: 50%; left: 0; top: 0;
  transition: width 0.4s cubic-bezier(0.19, 1, 0.22, 1), height 0.4s cubic-bezier(0.19, 1, 0.22, 1);
}
.cursor-ring.is-active { width: 60px; height: 60px; background: rgba(226, 217, 200, 0.1); }
.cursor-canvas { position: absolute; inset: 0; z-index: -1; }
</style>