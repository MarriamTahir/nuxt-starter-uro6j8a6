<template>
  <div id="ImaginePossible" :style="{ '--progress': progress }">
    <CustomCursor />
    <div class="noise-overlay"></div>

    <header class="minimal-nav">
      <div class="logo-group">
        <span class="logo-text">The Obsidian Assembly</span>
        <span class="tagline-small">Imagine Possible</span>
      </div>

      <div class="nav-center">
        <button class="pill-btn interactive">Places</button>
        <div class="nav-divider"></div>
        <button class="pill-btn interactive">Objects</button>
      </div>

      <div class="nav-right">
        <div class="burger-menu">
          <div class="lines"><span></span><span></span></div>
          <p>MENU</p>
        </div>
      </div>
    </header>

    <main class="main-content">
      <section class="hero-v2">
        <div class="side-col left">
          <p>
            A Private Assembly <br />
            for Makers
          </p>
        </div>

        <div class="center-titles">
          <h1 class="serif-title">Nothing</h1>
          <h1 class="serif-title -italic">Shown</h1>
          <h1 class="serif-title">First</h1>
        </div>

        <div class="side-col right">
          <p>
            Coordinates <br />
            Withheld
          </p>
        </div>
      </section>

      <div class="visual-center">
        <div class="image-wrapper-reveal">
          <img
            src="https://placehold.co/800x1000/2a2a2a/f1eade?text=Obsidian+Artifact"
            alt="Central Piece"
            class="main-artifact"
          />
        </div>
        <div class="bottom-branding">
          <p class="commitment-text">Commitment Precedes</p>
          <p class="brand-footer">IMAGINE POSSIBLE</p>
        </div>
      </div>

      <section class="projects-grid">
        <ProjectCard
          v-for="(project, index) in projects"
          :key="index"
          :title="project.title"
          :category="project.category"
          :year="project.year"
          :index="index"
        />
      </section>
    </main>

    <MainFooter />
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue';
import CustomCursor from '~/components/CustomCursor.vue';
import MainFooter from '~/components/MainFooter.vue';
import ProjectCard from '~/components/ProjectCard.vue';

const progress = ref(0);

const projects = [
  { title: 'Mineral Trading App', category: 'Product Design', year: '2024' },
  { title: 'Tutor Finder System', category: 'UX Research', year: '2023' },
  { title: 'E-commerce Experience', category: 'UI/UX Design', year: '2024' },
  { title: 'SofTech Branding', category: 'Visual Identity', year: '2023' },
];

const updateProgress = () => {
  const scrollY = window.scrollY;
  const maxScroll = document.documentElement.scrollHeight - window.innerHeight;
  progress.value = maxScroll > 0 ? scrollY / maxScroll : 0;
};

onMounted(() => {
  window.addEventListener('scroll', updateProgress);
  updateProgress();
});

onUnmounted(() => {
  window.removeEventListener('scroll', updateProgress);
});
</script>

<style>
/* --- DESIGN SYSTEM (SCREENSHOT ACCURATE) --- */
:root {
  --bg-stone-light: #c3b4a2;
  --bg-stone-dark: #8e7d6a;
  --c-text: #f1eade;
  --f-serif: 'Cormorant Garamond', serif;
  --f-sans: 'Inter', sans-serif;
  --f-cubic: cubic-bezier(0.35, 0.35, 0, 1);
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  cursor: none !important;
}

body {
  background: linear-gradient(
    180deg,
    var(--bg-stone-light) 0%,
    var(--bg-stone-dark) 100%
  );
  background-attachment: fixed;
  color: var(--c-text);
  font-family: var(--f-sans);
  overflow-x: hidden;
  -webkit-font-smoothing: antialiased;
}

/* --- NOISE OVERLAY --- */
.noise-overlay {
  position: fixed;
  inset: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
  z-index: 9999;
  opacity: 0.12;
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='160' height='160'%3E%3Cfilter id='a'%3E%3CfeTurbulence baseFrequency='.9' numOctaves='2' stitchTiles='stitch' type='fractalNoise'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23a)'/%3E%3C/svg%3E");
}

/* --- NAVIGATION --- */
.minimal-nav {
  position: fixed;
  top: 0;
  width: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 30px 4vw;
  z-index: 100;
}

.logo-group {
  display: flex;
  flex-direction: column;
}
.logo-text {
  font-family: var(--f-serif);
  font-size: 1.2rem;
}
.tagline-small {
  font-size: 0.6rem;
  text-transform: uppercase;
  letter-spacing: 0.2em;
  opacity: 0.6;
}

.nav-center {
  display: flex;
  align-items: center;
  background: rgba(255, 255, 255, 0.05);
  backdrop-filter: blur(10px);
  border-radius: 8px;
  padding: 4px;
}

.pill-btn {
  background: transparent;
  border: none;
  color: white;
  padding: 8px 25px;
  font-size: 10px;
  text-transform: uppercase;
  letter-spacing: 0.1em;
}

.nav-divider {
  width: 1px;
  height: 15px;
  background: rgba(255, 255, 255, 0.2);
}

.burger-menu {
  display: flex;
  align-items: center;
  gap: 15px;
  background: #f1eade;
  color: #151415;
  padding: 8px 15px;
  border-radius: 8px;
}
.burger-menu p {
  font-size: 10px;
  font-weight: 700;
  letter-spacing: 0.1em;
}
.lines {
  display: flex;
  flex-direction: column;
  gap: 4px;
}
.lines span {
  width: 20px;
  height: 1px;
  background: #151415;
}

/* --- HERO SECTION --- */
.hero-v2 {
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0 6vw;
  position: relative;
}

.serif-title {
  font-family: var(--f-serif);
  font-size: clamp(4rem, 15vw, 18rem);
  font-weight: 300;
  line-height: 0.75;
  text-align: center;
}

.-italic {
  font-style: italic;
  transform: translateX(10vw);
}

.side-col {
  font-size: 11px;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  line-height: 1.6;
  opacity: 0.8;
}

/* --- VISUAL CENTER --- */
.visual-center {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: -10vh;
}

.main-artifact {
  width: 100%;
  max-width: 450px;
  filter: drop-shadow(0 30px 60px rgba(0, 0, 0, 0.3));
  transition: transform 0.5s var(--f-cubic);
}

.bottom-branding {
  text-align: center;
  margin-top: 40px;
}
.commitment-text {
  font-family: var(--f-serif);
  font-size: 2rem;
}
.brand-footer {
  font-size: 0.6rem;
  letter-spacing: 0.5em;
  opacity: 0.5;
  margin-top: 10px;
}

/* --- GRID --- */
.projects-grid {
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  gap: 4vw;
  padding: 100px 6vw;
}

/* Animations */
::selection {
  background: var(--c-text);
  color: var(--bg-stone-dark);
}
</style>
