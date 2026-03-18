<template>
  <footer class="obsidian-footer">
    <div class="footer-top">
      <div class="brand-desc">
        <h2 class="serif-footer-logo">The Obsidian Assembly</h2>
        <p class="mission-text">
          Imagine Possible is a design exploration initiative by Fiddle Digital,
          operating across various locations and disciplines.
        </p>
      </div>

      <div class="footer-nav">
        <div class="nav-group">
          <p class="nav-label">General</p>
          <a href="#">Places</a>
          <a href="#">Objects</a>
          <a href="#">People</a>
        </div>
        <div class="nav-group">
          <p class="nav-label">Connect</p>
          <a href="#">About</a>
          <a href="#">Contact</a>
          <a href="#" class="no-social">No Social Medias</a>
        </div>
      </div>
    </div>

    <div class="footer-bottom">
      <div class="bottom-left">© 2026</div>
      <div class="bottom-center">IMAGINE POSSIBLE</div>
      <div class="bottom-right">Website by Fiddle Digital</div>
    </div>
  </footer>
</template>

<style scoped>
.obsidian-footer {
  padding: 100px 6vw 40px;
  background: transparent; /* Background body gradient se aaye ga */
  color: var(--c-text);
  border-top: 1px solid rgba(255, 255, 255, 0.05);
}

.footer-top {
  display: flex;
  justify-content: space-between;
  margin-bottom: 80px;
  flex-wrap: wrap;
  gap: 40px;
}

.serif-footer-logo {
  font-family: var(--f-serif);
  font-size: 2.5rem;
  font-weight: 300;
  line-height: 1;
  margin-bottom: 20px;
}

.mission-text {
  max-width: 400px;
  font-size: 11px;
  line-height: 1.8;
  opacity: 0.6;
  text-transform: uppercase;
  letter-spacing: 0.1em;
}

.footer-nav {
  display: flex;
  gap: 100px;
}

.nav-label {
  font-size: 10px;
  text-transform: uppercase;
  letter-spacing: 0.2em;
  margin-bottom: 25px;
  opacity: 0.4;
}

.nav-group a {
  display: block;
  color: var(--c-text);
  text-decoration: none;
  font-size: 12px;
  margin-bottom: 12px;
  font-family: var(--f-serif);
  font-style: italic;
  transition: opacity 0.3s ease;
}

.nav-group a:hover {
  opacity: 0.5;
}

.footer-bottom {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding-top: 30px;
  border-top: 1px solid rgba(255, 255, 255, 0.1);
  font-size: 10px;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  opacity: 0.5;
}

.bottom-center {
  letter-spacing: 0.5em;
  font-weight: 600;
}

@media (max-width: 768px) {
  .footer-top {
    flex-direction: column;
  }
  .footer-nav {
    gap: 50px;
  }
  .footer-bottom {
    flex-direction: column;
    gap: 20px;
    text-align: center;
  }
}
</style>
