<template>
  <NuxtLink v-if="to" :to="to" class="btn-wrap" :class="{ '-big': big }">
    <div class="btn-bg-layer"></div>
    <div class="btn-content">
      <span class="btn-text">
        <span class="text-original">{{ text }}</span>
        <span class="text-hover">{{ text }}</span>
      </span>
      <div class="btn-dot"></div>
    </div>
  </NuxtLink>
</template>

<script setup>
defineProps({ text: String, to: String, big: Boolean });
</script>

<style scoped>
.btn-wrap {
  --c-stone: #e2d9c8;
  --c-dark: #151415;
  --f-bezier: cubic-bezier(0.19, 1, 0.22, 1);

  display: inline-flex;
  position: relative;
  padding: 14px 32px;
  background-color: var(--c-stone);
  border-radius: 100px;
  overflow: hidden;
  isolation: isolate;
  text-decoration: none;
  transition: transform 0.6s var(--f-bezier);
  cursor: none;
}

.btn-wrap.-big {
  padding: 20px 48px;
}

.btn-bg-layer {
  position: absolute;
  inset: 0;
  background-color: var(--c-dark);
  clip-path: inset(100% 0 0 0);
  transition: transform 0.6s var(--f-bezier);
  z-index: -1;
}

.btn-wrap:hover .btn-bg-layer {
  transform: translateY(0);
}
.btn-wrap:hover {
  transform: scale(1.05);
}

.btn-content {
  position: relative;
  display: flex;
  align-items: center;
  gap: 12px;
  pointer-events: none;
}

.btn-text {
  display: block;
  height: 1.2em;
  overflow: hidden;
  position: relative;
  font-weight: 500;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  font-size: 13px;
}

.text-original,
.text-hover {
  display: block;
  transition: transform 0.6s var(--f-bezier);
  color: var(--c-dark);
}

.text-hover {
  position: absolute;
  top: 100%;
  left: 0;
  width: 100%;
  color: var(--c-stone);
}

.btn-wrap:hover .text-original {
  transform: translateY(-100%);
}
.btn-wrap:hover .text-hover {
  transform: translateY(-100%);
}

.btn-dot {
  width: 6px;
  height: 6px;
  background: var(--c-dark);
  border-radius: 50%;
  transition: all 0.6s var(--f-bezier);
}

.btn-wrap:hover .btn-dot {
  background: var(--c-stone);
  transform: scale(1.3);
}
</style>
