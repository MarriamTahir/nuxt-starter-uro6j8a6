<template>
  <div class="luxury-container">
    <header class="luxury-nav">
      <div class="logo-group">
        <span class="studio-name">RiamStudio</span>
        <span class="designer-name">Marriam Tahir</span>
      </div>

      <nav class="nav-links">
        <BaseButton text="Work" routeurl="/work" :reverse="true" />
        <BaseButton text="About" routeurl="/about" :reverse="true" />
        <div class="contact-pill interactive">
          <span>Let's Talk</span>
        </div>
      </nav>
    </header>

    <main class="hero-section">
      <div class="hero-content">
        <div class="reveal-mask">
          <p class="overline">UI/UX DESIGN & STRATEGY</p>
        </div>
        <div class="reveal-mask">
          <h1 class="main-title">Designing <span class="italic-blue">Intentional</span></h1>
        </div>
        <div class="reveal-mask">
          <h1 class="main-title">Experiences.</h1>
        </div>
        
        <div class="hero-footer">
          <p class="description">
            Specializing in high-end digital products at RiamStudio. 
            Focusing on the intersection of user psychology and minimalist aesthetics.
          </p>
          <div class="scroll-indicator">
            <span class="line"></span>
            <span class="txt">SCROLL</span>
          </div>
        </div>
      </div>
    </main>
  </div>
</template>

<style scoped>
.luxury-container {
  min-height: 100vh;
  background-color: #FBFBFB; /* Luxury White */
  color: #151415; /* Obsidian Black */
}

/* NAVIGATION */
.luxury-nav {
  position: fixed;
  top: 0; width: 100%;
  display: flex; justify-content: space-between; align-items: center;
  padding: 40px 6vw;
  z-index: 100;
}

.logo-group {
  display: flex;
  flex-direction: column;
}

.studio-name {
  font-family: 'Tenor Sans', sans-serif;
  font-size: 1.5rem;
  letter-spacing: -0.02em;
  color: #002D62; /* Navy Blue */
}

.designer-name {
  font-size: 10px;
  text-transform: uppercase;
  letter-spacing: 0.3em;
  opacity: 0.6;
  margin-top: 4px;
}

.nav-links {
  display: flex;
  align-items: center;
  gap: 20px;
}

.contact-pill {
  background: #002D62;
  color: #FBFBFB;
  padding: 12px 24px;
  border-radius: 100px;
  font-size: 11px;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  font-weight: 600;
}

/* HERO SECTION */
.hero-section {
  height: 100vh;
  display: flex;
  align-items: center;
  padding: 0 6vw;
}

.reveal-mask {
  overflow: hidden;
}

.overline {
  font-size: 12px;
  letter-spacing: 0.4em;
  text-transform: uppercase;
  margin-bottom: 20px;
  color: #002D62;
  font-weight: 600;
}

.main-title {
  font-family: 'Tenor Sans', sans-serif;
  font-size: clamp(3rem, 8vw, 10rem);
  line-height: 1;
  font-weight: 400;
}

.italic-blue {
  font-style: italic;
  color: #002D62;
}

.hero-footer {
  margin-top: 60px;
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
}

.description {
  max-width: 400px;
  font-size: 16px;
  line-height: 1.6;
  opacity: 0.8;
}

.scroll-indicator {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 15px;
}

.line {
  width: 1px;
  height: 60px;
  background: #002D62;
  transform-origin: top;
  animation: scaleLine 2s infinite ease-in-out;
}

.txt {
  font-size: 10px;
  letter-spacing: 0.2em;
}

@keyframes scaleLine {
  0% { transform: scaleY(0); }
  50% { transform: scaleY(1); }
  100% { transform: scaleY(0); transform-origin: bottom; }
}
</style>