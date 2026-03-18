<template>
  <div class="project-card" :class="{ '-offset': index % 2 !== 0 }">
    <div class="card-inner">
      <div class="image-container">
        <img
          src="https://placehold.co/800x1000/2a2a2a/f1eade?text=Project+Work"
          alt="Project Image"
          class="project-img"
        />
        <div class="overlay-info">
          <span>View Project</span>
        </div>
      </div>

      <div class="project-details">
        <h3 class="project-title">{{ title }}</h3>
        <div class="project-meta">
          <span class="category">{{ category }}</span>
          <span class="dot"></span>
          <span class="year">{{ year }}</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
defineProps({
  title: String,
  category: String,
  year: String,
  index: Number,
});
</script>

<style scoped>
.project-card {
  grid-column: span 6; /* Do cards side-by-side */
  margin-bottom: 10vh;
  transition: transform 0.8s var(--f-cubic);
}

/* Staggered Effect: Right side cards are lower */
.-offset {
  margin-top: 15vh;
}

.image-container {
  position: relative;
  width: 100%;
  aspect-ratio: 4/5;
  overflow: hidden;
  background: rgba(0, 0, 0, 0.1);
  border-radius: 2px;
}

.project-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 1.2s var(--f-cubic);
  filter: grayscale(20%);
}

.image-container:hover .project-img {
  transform: scale(1.05);
}

.overlay-info {
  position: absolute;
  inset: 0;
  background: rgba(142, 125, 106, 0.4);
  display: flex;
  align-items: center;
  justify-content: center;
  opacity: 0;
  transition: opacity 0.4s ease;
  backdrop-filter: blur(5px);
}

.image-container:hover .overlay-info {
  opacity: 1;
}

.overlay-info span {
  text-transform: uppercase;
  font-size: 10px;
  letter-spacing: 0.2em;
  border: 1px solid white;
  padding: 10px 20px;
}

.project-details {
  margin-top: 25px;
}

.project-title {
  font-family: var(--f-serif);
  font-size: 1.8rem;
  font-weight: 300;
  font-style: italic;
  margin-bottom: 8px;
}

.project-meta {
  display: flex;
  align-items: center;
  gap: 12px;
  font-size: 10px;
  text-transform: uppercase;
  letter-spacing: 0.15em;
  opacity: 0.6;
}

.dot {
  width: 3px;
  height: 3px;
  background: var(--c-text);
  border-radius: 50%;
}

/* Mobile adjustments */
@media (max-width: 768px) {
  .project-card {
    grid-column: span 12;
  }
  .-offset {
    margin-top: 0;
  }
}
</style>
