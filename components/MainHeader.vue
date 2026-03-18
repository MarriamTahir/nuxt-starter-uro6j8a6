<template>
  <header :class="{ '-scrolled': isScrolled }">
    <div class="header-container">
      <div class="logo">
        <span class="t-the">The</span>
        <span class="t-obsidian">Obsidian</span>
        <span class="t-assembly">Assembly</span>
      </div>

      <nav class="nav-links">
        <span class="link">Portfolio</span>
        <span class="link">About</span>
        <span class="link -disabled">Contact</span>
      </nav>

      <div class="actions">
        <button class="menu-trigger">Menu</button>
      </div>
    </div>
  </header>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue';

const isScrolled = ref(false);
const handleScroll = () => {
  isScrolled.value = window.scrollY > 50;
};

onMounted(() => window.addEventListener('scroll', handleScroll));
onUnmounted(() => window.removeEventListener('scroll', handleScroll));
</script>

<style scoped>
header {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  z-index: 100;
  padding: 1.5rem 2rem;
  color: var(--c-yellow);
  background-image: linear-gradient(
    180deg,
    rgba(0, 0, 0, 0.8) 0%,
    transparent 100%
  );
  transition: all 0.5s var(--f-cubic);
}

header.-scrolled {
  color: var(--c-white);
  padding: 1rem 2rem;
  backdrop-filter: blur(10px);
}

.header-container {
  max-width: 1400px;
  margin: 0 auto;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.logo {
  display: flex;
  flex-direction: column;
  line-height: 0.9;
  font-weight: 700;
  text-transform: uppercase;
  font-size: 1rem;
}

.t-the {
  margin-left: 0.5em;
  font-size: 0.8em;
}
.t-assembly {
  margin-left: 0.8em;
}

.nav-links {
  display: flex;
  gap: 2rem;
}
.link {
  font-size: 0.7rem;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  opacity: 0.7;
  cursor: pointer;
}

.link.-disabled {
  opacity: 0.2;
  cursor: not-allowed;
}

.menu-trigger {
  background: transparent;
  border: 1px solid currentColor;
  color: currentColor;
  padding: 0.4rem 1rem;
  border-radius: 2rem;
  text-transform: uppercase;
  font-size: 0.6rem;
  cursor: pointer;
}
</style>
