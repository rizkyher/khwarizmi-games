<script lang="ts">
  import { Play, Sparkles, MousePointer2 } from "@lucide/svelte";

  let mouseY = $state(0);
  let mouseX = $state(0);

  function handleMouseMove(e: MouseEvent) {
    mouseX = (e.clientX / window.innerWidth - 0.5) * 30;
    mouseY = (e.clientY / window.innerHeight - 0.5) * 30;
  }
</script>

<section onmousemove={handleMouseMove} role="region" aria-label="Khwarizmi Games Hero Section" class="hero-section">
  <!-- Background Blobs -->
  <div class="absolute inset-0 pointer-events-none overflow-hidden">
    <div class="blob blob-1" style="transform: translate({mouseX * -0.8}px, {mouseY * -0.8}px)"></div>
    <div class="blob blob-2" style="transform: translate({mouseX * 0.8}px, {mouseY * 0.8}px)"></div>

    <!-- Floating Clouds -->
    <div class="cloud cloud-1" style="transform: translateX({mouseX * 0.3}px) translateY({mouseY * 0.3}px)">☁️</div>
    <div class="cloud cloud-2" style="transform: translateX({mouseX * -0.5}px) translateY({mouseY * -0.5}px)">☁️</div>
    <div class="cloud cloud-3" style="transform: translateX({mouseX * 0.7}px) translateY({mouseY * 0.7}px)">☁️</div>
    <div class="cloud cloud-4" style="transform: translateX({mouseX * 0.4}px) translateY({mouseY * 0.4}px)">☁️</div>
    <div class="cloud cloud-5" style="transform: translateX({mouseX * -0.6}px) translateY({mouseY * -0.6}px)">☁️</div>

    <!-- Spirit Dust Particles -->
    {#each Array(30) as _, i}
      <div
        class="spirit-dust"
        style="
          left: {Math.random() * 100}%; 
          top: {Math.random() * 100}%; 
          animation-delay: {Math.random() * 10}s;
          color: {['#fefae0', '#d9e4dd', '#e4e9be'][Math.floor(Math.random() * 3)]};
          transform: scale({Math.random() * 0.5 + 0.5});
        "
      >
        ✨
      </div>
    {/each}
  </div>

  <!-- Main Content -->
  <div class="content-wrapper">
    <!-- Header Badge -->
    <div class="badge-wrapper">
      <div class="badge">
        <span class="badge-text">
          <Sparkles size={14} class="animate-spin-slow" />
          EST. 2024 // SPIRIT_REALM
          <Sparkles size={14} class="animate-spin-slow" />
        </span>
      </div>
    </div>

    <!-- Title -->
    <div class="title-wrapper">
      <h1 class="main-title">
        <span class="title-line">Khwarizmi</span>
        <span class="title-line subtitle">Games</span>
      </h1>
      <div class="butterfly" style="transform: translate({mouseX * 1.2}px, {mouseY * 1.2}px)">🦋</div>
    </div>

    <!-- Description & CTA -->
    <div class="description-wrapper">
      <p class="description">
        A digital archive where <span class="highlight">imagination</span> meets the warmth of watercolor and pixel craftsmanship.
      </p>

      <div class="cta-section">
        <button class="cta-button">
          <span class="cta-content">
            <Play size={24} fill="currentColor" />
            ENTER_PARK
          </span>
          <div class="cta-overlay"></div>
        </button>

        <div class="mouse-hint">
          <MousePointer2 size={18} />
          <span>Move to stir the breeze</span>
        </div>
      </div>
    </div>
  </div>

  <!-- Footer Landscape -->
  <div class="footer-landscape">
    <!-- Hills -->
    <div class="hills" style="transform: translateX({mouseX * 0.2}px)"></div>

    <!-- Ground -->
    <div class="ground">
      <div class="ground-pattern"></div>

      <!-- Grass -->
      <div class="grass-container">
        {#each Array(20) as _, i}
          <div class="grass" style="left: {i * 5}%; animation-delay: {i * 0.5}s; transform: translateX({mouseX * 0.1}px)">🌱</div>
        {/each}
      </div>

      <!-- Mushrooms -->
      <div class="mushroom-container">
        {#each Array(8) as _, i}
          <span class="mushroom" style="animation-delay: {i * 0.4}s; transform: translateY({Math.sin(i) * 10}px)">🍄</span>
        {/each}
      </div>
    </div>
  </div>

  <!-- Texture Overlays -->
  <div class="texture-overlay texture-paper"></div>
  <div class="texture-overlay texture-dots"></div>
</section>

<style>
  /* Variables */
  :root {
    --color-bg-light: #f1f0e8;
    --color-bg-dark: #e0e7d7;
    --color-cream: #fdf6e3;
    --color-dark: #2d2d2d;
    --color-forest: #283618;
    --color-sage: #606c38;
    --color-brown: #bc6c25;
    --color-mint: #d9e4dd;
    --color-pale: #e4e9be;
  }

  /* Main Section */
  .hero-section {
    position: relative;
    min-height: 100vh;
    background: linear-gradient(to bottom, var(--color-bg-light), var(--color-bg-dark));
    overflow: hidden;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding-top: 5rem;
    cursor: crosshair;
    image-rendering: pixelated;
  }

  /* Background Blobs */
  .blob {
    position: absolute;
    filter: blur(100px);
    animation: pulse 3s ease-in-out infinite;
  }

  .blob-1 {
    top: 15%;
    left: 10%;
    width: 24rem;
    height: 12rem;
    background: var(--color-mint);
    opacity: 0.4;
  }

  .blob-2 {
    bottom: 20%;
    right: 10%;
    width: 20rem;
    height: 10rem;
    background: var(--color-pale);
    opacity: 0.3;
    filter: blur(80px);
    animation-delay: 1s;
  }

  /* Floating Clouds */
  .cloud {
    position: absolute;
    font-size: 6rem;
    opacity: 0.3;
    user-select: none;
    pointer-events: none;
  }

  .cloud-1 {
    top: 10%;
    left: -20%;
    font-size: 9rem;
    animation: driftRight 40s linear infinite;
  }

  .cloud-2 {
    top: 30%;
    right: -15%;
    font-size: 8rem;
    opacity: 0.25;
    animation: driftLeft 50s linear infinite;
  }

  .cloud-3 {
    bottom: 50%;
    left: 20%;
    font-size: 7rem;
    opacity: 0.2;
    animation: driftRight 45s linear infinite 10s;
  }

  .cloud-4 {
    top: 60%;
    right: 10%;
    font-size: 6rem;
    opacity: 0.18;
    animation: driftLeft 55s linear infinite 15s;
  }

  .cloud-5 {
    top: 45%;
    left: 5%;
    font-size: 6.5rem;
    opacity: 0.22;
    animation: driftRight 48s linear infinite 20s;
  }

  /* Spirit Dust */
  .spirit-dust {
    position: absolute;
    font-size: 1.25rem;
    opacity: 0;
    animation: spiritDust 10s linear infinite;
  }

  /* Content */
  .content-wrapper {
    position: relative;
    z-index: 20;
    text-align: center;
    padding: 0 1.5rem;
  }

  /* Badge */
  .badge-wrapper {
    display: inline-block;
    margin-bottom: 2.5rem;
  }

  .badge {
    position: relative;
    background: var(--color-cream);
    border: 3px solid var(--color-forest);
    padding: 0.5rem 1.5rem;
    box-shadow: 4px 4px 0 0 var(--color-brown);
    transition: all 0.3s ease;
  }

  .badge-wrapper:hover .badge {
    transform: translate(1px, 1px);
    box-shadow: none;
  }

  .badge-text {
    font-family: "VT323", monospace;
    color: var(--color-sage);
    letter-spacing: 0.3em;
    font-size: 0.875rem;
    text-transform: uppercase;
    display: flex;
    align-items: center;
    gap: 0.75rem;
  }

  /* Title */
  .title-wrapper {
    position: relative;
    margin-bottom: 2.5rem;
  }

  .main-title {
    font-family: "VT323", monospace;
    font-size: 6rem;
    color: var(--color-dark);
    line-height: 0.85;
    letter-spacing: -0.05em;
    text-transform: uppercase;
    user-select: none;
    -webkit-text-stroke: 2px var(--color-dark);
    paint-order: stroke fill;
  }

  @media (min-width: 768px) {
    .main-title {
      font-size: 10rem;
    }
  }

  .title-line {
    display: block;
    filter: drop-shadow(6px 6px 0 var(--color-cream));
  }

  .subtitle {
    color: var(--color-sage);
    font-style: italic;
  }

  .butterfly {
    position: absolute;
    top: -2.5rem;
    right: -1rem;
    font-size: 3rem;
    animation: float 4s ease-in-out infinite;
  }

  /* Description */
  .description-wrapper {
    max-width: 36rem;
    margin: 0 auto;
    display: flex;
    flex-direction: column;
    gap: 2rem;
  }

  .description {
    font-family: "VT323", monospace;
    font-size: 1.5rem;
    color: rgba(93, 64, 55, 0.8);
    line-height: 1.375;
    text-transform: uppercase;
    letter-spacing: -0.025em;
  }

  .highlight {
    background: rgba(96, 108, 56, 0.1);
    padding: 0 0.5rem;
    font-style: italic;
    color: var(--color-sage);
  }

  /* CTA Section */
  .cta-section {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 1.5rem;
  }

  .cta-button {
    position: relative;
    background: var(--color-dark);
    border: 4px solid var(--color-forest);
    padding: 1.25rem 3rem;
    box-shadow: 8px 8px 0 0 var(--color-brown);
    transition: all 0.3s ease;
    overflow: hidden;
    cursor: pointer;
  }

  .cta-button:hover {
    box-shadow: none;
    transform: translate(1px, 1px);
  }

  .cta-button:active {
    transform: scale(0.95);
  }

  .cta-content {
    position: relative;
    z-index: 10;
    font-family: "VT323", monospace;
    font-size: 1.875rem;
    color: var(--color-bg-light);
    display: flex;
    align-items: center;
    gap: 1rem;
  }

  .cta-overlay {
    position: absolute;
    inset: 0;
    background: var(--color-sage);
    transform: translateX(-100%);
    transition: transform 0.5s ease;
  }

  .cta-button:hover .cta-overlay {
    transform: translateX(0);
  }

  /* Mouse Hint */
  .mouse-hint {
    display: flex;
    align-items: center;
    gap: 0.75rem;
    color: rgba(188, 108, 37, 0.6);
    font-family: "VT323", monospace;
    font-size: 1.25rem;
    text-transform: uppercase;
    animation: pulse 2s ease-in-out infinite;
  }

  /* Footer Landscape */
  .footer-landscape {
    position: absolute;
    bottom: 0;
    width: 100%;
    z-index: 30;
    pointer-events: none;
  }

  .hills {
    height: 12rem;
    width: 100%;
    background: rgba(217, 228, 221, 0.6);
    clip-path: polygon(0 100%, 0 45%, 15% 30%, 35% 55%, 55% 20%, 75% 50%, 90% 15%, 100% 40%, 100% 100%);
    transition: transform 0.3s ease;
  }

  .ground {
    position: relative;
    height: 7rem;
    background: linear-gradient(to top, var(--color-sage), #7a8a4e);
    border-top: 6px solid var(--color-dark);
  }

  .ground-pattern {
    position: absolute;
    inset: 0;
    background-image: radial-gradient(var(--color-dark) 2px, transparent 2px);
    background-size: 32px 32px;
    opacity: 0.05;
  }

  /* Grass */
  .grass-container {
    position: absolute;
    inset: 0;
    overflow: hidden;
  }

  .grass {
    position: absolute;
    bottom: 0;
    font-size: 1.875rem;
    opacity: 0.7;
    animation: swayGrass 15s ease-in-out infinite;
  }

  /* Mushrooms */
  .mushroom-container {
    display: flex;
    justify-content: space-around;
    align-items: center;
    height: 100%;
    max-width: 64rem;
    margin: 0 auto;
    opacity: 0.6;
    position: relative;
    z-index: 10;
  }

  .mushroom {
    font-size: 1.5rem;
    animation: bounce 1s ease-in-out infinite;
  }

  /* Texture Overlays */
  .texture-overlay {
    position: absolute;
    inset: 0;
    pointer-events: none;
  }

  .texture-paper {
    mix-blend-mode: multiply;
    opacity: 0.2;
    background-image: url("https://www.transparenttextures.com/patterns/p6.png");
  }

  .texture-dots {
    opacity: 0.1;
    background-image: radial-gradient(#000 1px, transparent 1px);
    background-size: 20px 20px;
  }

  /* Animations */
  @keyframes driftRight {
    0% {
      transform: translateX(-100vw);
    }
    100% {
      transform: translateX(100vw);
    }
  }

  @keyframes driftLeft {
    0% {
      transform: translateX(100vw);
    }
    100% {
      transform: translateX(-100vw);
    }
  }

  @keyframes floatSlow {
    0%,
    100% {
      transform: translate(0, 0);
    }
    50% {
      transform: translate(50px, -20px);
    }
  }

  @keyframes floatMedium {
    0%,
    100% {
      transform: translate(0, 0);
    }
    50% {
      transform: translate(-40px, 30px);
    }
  }

  @keyframes floatFast {
    0%,
    100% {
      transform: translate(0, 0);
    }
    50% {
      transform: translate(60px, -15px);
    }
  }

  @keyframes spiritDust {
    0% {
      transform: translateY(100vh) translateX(0) scale(0.5);
      opacity: 0;
    }
    10% {
      opacity: 0.8;
    }
    80% {
      opacity: 0.8;
    }
    100% {
      transform: translateY(-10vh) translateX(50px) scale(1);
      opacity: 0;
    }
  }

  @keyframes swayGrass {
    0%,
    100% {
      transform: rotateZ(0deg) scaleY(1);
    }
    25% {
      transform: rotateZ(-3deg) scaleY(1.05);
    }
    50% {
      transform: rotateZ(0deg) scaleY(1);
    }
    75% {
      transform: rotateZ(3deg) scaleY(1.05);
    }
  }

  @keyframes float {
    0%,
    100% {
      transform: translateY(0);
    }
    50% {
      transform: translateY(-20px);
    }
  }

  @keyframes pulse {
    0%,
    100% {
      opacity: inherit;
    }
    50% {
      opacity: calc(inherit * 0.7);
    }
  }

  @keyframes bounce {
    0%,
    100% {
      transform: translateY(0);
    }
    50% {
      transform: translateY(-10px);
    }
  }

  .animate-spin-slow {
    animation: spin 8s linear infinite;
  }

  @keyframes spin {
    from {
      transform: rotate(0deg);
    }
    to {
      transform: rotate(360deg);
    }
  }

  /* Performance Optimization */
  div,
  span {
    will-change: transform, opacity;
  }
</style>
