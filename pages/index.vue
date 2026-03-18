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
        <div class="burger-menu interactive">
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
          <div class="mask"><h1 class="serif-title">Nothing</h1></div>
          <div class="mask"><h1 class="serif-title -italic">Shown</h1></div>
          <div class="mask"><h1 class="serif-title">First</h1></div>
        </div>

        <div class="side-col right">
          <p>
            Coordinates <br />
            Withheld
          </p>
        </div>
      </section>

      <div class="visual-center">
        <div
          class="image-wrapper-reveal"
          :style="{ transform: `translateY(${-progress * 50}px)` }"
        >
          <img
            src="https://placehold.co/800x1000/2a2a2a/f1eade?text=Obsidian+Artifact"
            alt="Central Piece"
            class="main-artifact"
          />
        </div>
        <div class="bottom-branding">
          <p class="commitment-text">Commitment Precedes</p>
          <p class="brand-footer">IMAGINE POSSIBLE</p>
          <div class="mt-10">
            <BaseButton text="Explore Archive" to="/work" :big="true" />
          </div>
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
// Components import logic handles cursor & buttons

const progress = ref(0);
const projects = [
  { title: 'Mineral Trading App', category: 'Product', year: '2024' },
  { title: 'Tutor Finder System', category: 'UX', year: '2023' },
  { title: 'E-commerce Exp', category: 'UI/UX', year: '2024' },
  { title: 'SofTech Branding', category: 'Visual', year: '2023' },
];

const handleScroll = () => {
  const totalHeight =
    document.documentElement.scrollHeight - window.innerHeight;
  progress.value = window.scrollY / totalHeight;
};

onMounted(() => {
  window.addEventListener('scroll', handleScroll);
});
onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll);
});
</script>

<style scoped>
/* Scoped styles use karein taake conflicts na hon */
.home-page {
  --c-stone-light: #c3b4a2;
  --c-stone-dark: #8e7d6a;
  background: linear-gradient(
    180deg,
    var(--c-stone-light),
    var(--c-stone-dark)
  );
}

.noise-overlay {
  position: fixed;
  inset: 0;
  z-index: 999;
  opacity: 0.08;
  pointer-events: none;
  background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.65' numOctaves='3' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E");
}

.center-titles {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.mask {
  overflow: hidden;
  height: 1.1em;
}

.serif-title {
  font-family: 'Cormorant Garamond', serif;
  font-size: clamp(4rem, 12vw, 15rem);
  font-weight: 300;
  line-height: 0.8;
  color: #f1eade;
  /* Entrance Animation */
  transform: translateY(100%);
  animation: reveal 1.5s cubic-bezier(0.19, 1, 0.22, 1) forwards;
}

.-italic {
  font-style: italic;
  transform: translateX(5vw) translateY(100%);
}

@keyframes reveal {
  to {
    transform: translateY(0);
  }
}

.mt-10 {
  margin-top: 40px;
}

/* Grid layout fix */
.projects-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 20px;
  padding: 100px 6vw;
}

@media (max-width: 768px) {
  .projects-grid {
    grid-template-columns: 1fr;
  }
}
</style>
