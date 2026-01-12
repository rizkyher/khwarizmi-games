<script lang="ts">
  import Navbar from "$lib/components/ui/navbar/Navbar.svelte";
  import Hero from "$lib/components/ui/hero/Hero.svelte";
  import GameList from "$lib/components/ui/game/GameList.svelte";
  import GameFilter from "$lib/components/ui/game/GameFilter.svelte";
  import DevShowcase from "$lib/components/ui/game/DeveloperShowcase.svelte";
  import About from "$lib/components/ui/game/About.svelte";
  import Footer from "$lib/components/ui/footer/Footer.svelte";
  import { fade } from "svelte/transition";

  // Svelte 5 State
  let activeCategory = $state("All Games");
  let scrollY = $state(0);

  function handleScroll() {
    scrollY = window.scrollY;
  }
</script>

<svelte:window onscroll={handleScroll} />

<svelte:head>
  <title>GHP Studio | Spirit of Pixel</title>
  <style>
    @import url("https://fonts.googleapis.com/css2?family=VT323&display=swap");

    :root {
      --ghibli-grass: #606c38;
      --ghibli-cream: #fefae0;
      --ghibli-wood: #bc6c25;
      --ghibli-sand: #f1f0e8;
      --ghibli-sky: #a8dadc;
      --ghibli-forest: #283618;
      --ghibli-moss: #7a8a4e;
    }

    body {
      background-color: var(--ghibli-sand);
      font-family: "VT323", monospace;
      image-rendering: pixelated;
      margin: 0;
      overflow-x: hidden;
    }

    /* Scrollbar Ghibli Style */
    ::-webkit-scrollbar {
      width: 14px;
    }
    ::-webkit-scrollbar-track {
      background: linear-gradient(to bottom, var(--ghibli-cream), var(--ghibli-sand));
      border-left: 2px solid var(--ghibli-forest);
    }
    ::-webkit-scrollbar-thumb {
      background: linear-gradient(to bottom, var(--ghibli-grass), var(--ghibli-wood));
      border: 3px solid var(--ghibli-cream);
      border-radius: 10px;
    }
    ::-webkit-scrollbar-thumb:hover {
      background: var(--ghibli-wood);
    }
  </style>
</svelte:head>

<div class="page-container">
  <!-- Animated Sky Background -->
  <div class="sky-atmosphere">
    <div class="sky-gradient"></div>

    <!-- Soft Ghibli Clouds -->
    {#each Array(8) as _, i}
      <div
        class="ghibli-cloud"
        style="
          left: {i * 18 - 15}%;
          top: {5 + (i % 4) * 12}%;
          animation-delay: {i * 4}s;
          animation-duration: {50 + i * 8}s;
          opacity: {0.3 + (i % 3) * 0.1};
        "
      >
        <svg viewBox="0 0 200 60" class="cloud-shape">
          <ellipse cx="35" cy="35" rx="35" ry="25" fill="white" opacity="0.8" />
          <ellipse cx="80" cy="28" rx="48" ry="32" fill="white" opacity="0.9" />
          <ellipse cx="130" cy="33" rx="42" ry="30" fill="white" opacity="0.85" />
          <ellipse cx="168" cy="37" rx="32" ry="23" fill="white" opacity="0.8" />
        </svg>
      </div>
    {/each}

    <!-- Flying Birds (Ghibli Style) -->
    {#each Array(6) as _, i}
      <div
        class="flying-bird"
        style="
          left: {-20 + Math.random() * 120}%;
          top: {8 + Math.random() * 35}%;
          animation-delay: {i * 3.5}s;
          animation-duration: {40 + i * 5}s;
        "
      >
        <svg viewBox="0 0 50 25" width="35" height="18" class="bird-silhouette">
          <path d="M5,12 Q12,7 20,12 T35,12 Q42,7 45,12" stroke="rgba(40, 54, 24, 0.4)" fill="none" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round" />
        </svg>
      </div>
    {/each}

    <!-- Floating Petals & Leaves -->
    {#each Array(25) as _, i}
      <div
        class="nature-particle"
        style="
          left: {Math.random() * 100}%;
          animation-delay: {Math.random() * 25}s;
          animation-duration: {18 + Math.random() * 12}s;
          font-size: {0.8 + Math.random() * 0.5}rem;
        "
      >
        {["🍃", "🌾", "🍂", "✨"][Math.floor(Math.random() * 4)]}
      </div>
    {/each}

    <!-- Light Rays (Subtle) -->
    <div class="light-rays-container">
      {#each Array(4) as _, i}
        <div
          class="sun-ray"
          style="
            left: {15 + i * 25}%;
            animation-delay: {i * 1.5}s;
            opacity: {0.03 + i * 0.01};
          "
        ></div>
      {/each}
    </div>
  </div>

  <!-- Watercolor Texture Overlay -->
  <div class="watercolor-texture"></div>

  <!-- Paper Grain -->
  <div class="paper-grain"></div>

  <Navbar bind:activeCategory />

  <main class="main-content">
    <section id="home">
      <Hero />
    </section>

    <!-- Game Archive Section with Ghibli Touch -->
    <section id="archive" class="archive-section">
      <!-- Decorative Nature Elements -->
      <div class="nature-sidebar">
        {#each [{ emoji: "🍂", delay: 0, duration: 4 }, { emoji: "🍄", delay: 1, duration: 5 }, { emoji: "🪵", delay: 2, duration: 4.5 }, { emoji: "🌿", delay: 1.5, duration: 5.5 }, { emoji: "🦋", delay: 0.5, duration: 6 }] as item, i}
          <span class="nature-icon" style="animation-delay: {item.delay}s; animation-duration: {item.duration}s;">
            {item.emoji}
          </span>
        {/each}
      </div>

      <!-- Floating Grass Blades (Background) -->
      <div class="grass-decoration">
        {#each Array(12) as _, i}
          <div
            class="grass-blade"
            style="
              left: {i * 8.5}%;
              animation-delay: {i * 0.3}s;
              height: {60 + Math.random() * 40}px;
            "
          ></div>
        {/each}
      </div>

      <div class="container mx-auto px-6 max-w-6xl relative z-10">
        <!-- Archive Header with Ghibli Aesthetic -->
        <div class="archive-header">
          <!-- Watercolor Splash Behind -->
          <div class="watercolor-splash"></div>

          <div class="header-content">
            <div class="header-badge">
              <span class="badge-dot"></span>
              Folder: Index_01
              <span class="badge-sparkle">✨</span>
            </div>

            <h2 class="archive-title">
              <span class="title-main">Game</span>
              <span class="title-accent">Library</span>
              <div class="title-underline"></div>
            </h2>

            <p class="filter-status">
              <span class="status-icon">📂</span>
              Filtering By: <span class="status-value">{activeCategory}</span>
            </p>
          </div>

          <div class="filter-container">
            <GameFilter bind:selected={activeCategory} />
          </div>
        </div>

        <!-- Game List -->
        <div class="game-list-wrapper" id="showcase">
          <GameList filter={activeCategory} />
        </div>
      </div>

      <!-- Decorative Hills at Bottom -->
      <div class="section-hills">
        <svg viewBox="0 0 1440 120" class="hills-svg">
          <path d="M0,80 Q240,40 480,60 T960,70 Q1200,50 1440,80 L1440,120 L0,120 Z" fill="rgba(122, 138, 78, 0.15)" />
          <path d="M0,90 Q360,60 720,80 T1440,90 L1440,120 L0,120 Z" fill="rgba(96, 108, 56, 0.1)" />
        </svg>
      </div>
    </section>

    <!-- Developer Showcase Section -->
    <section class="showcase-section">
      <!-- Dandelion Seeds Floating -->
      {#each Array.from({ length: 8 }) as _, i}
        <div
          class="dandelion-seed"
          style="
        left: {10 + i * 12}%;
        animation-delay: {i * 2}s;
      "
        >
          <svg viewBox="0 0 20 30" width="15" height="22">
            <circle cx="10" cy="3" r="2" fill="rgba(188,108,37,0.3)" />
            <line x1="10" y1="5" x2="10" y2="28" stroke="rgba(96,108,56,0.4)" stroke-width="0.5" />
            <circle cx="10" cy="28" r="1.5" fill="rgba(188,108,37,0.4)" />
          </svg>
        </div>
      {/each}

      <DevShowcase />
    </section>
    <section id="about">
      <About />
    </section>
  </main>

  <Footer />

  <!-- Atmospheric Vignette -->
  <div class="atmospheric-vignette"></div>

  <!-- Wind Effect Overlay -->
  <div class="wind-overlay"></div>
</div>

<style>
  /* ===== BASE LAYOUT ===== */
  .page-container {
    position: relative;
    min-height: 100vh;
    color: #283618;
    overflow: hidden;
  }

  :global(::selection) {
    background: #bc6c25;
    color: white;
  }

  /* ===== SKY ATMOSPHERE ===== */
  .sky-atmosphere {
    position: fixed;
    inset: 0;
    z-index: 0;
    pointer-events: none;
    overflow: hidden;
  }

  .sky-gradient {
    position: absolute;
    inset: 0;
    background: linear-gradient(to bottom, rgba(168, 218, 220, 0.15) 0%, rgba(254, 250, 224, 0.1) 40%, rgba(241, 240, 232, 0) 70%);
  }

  /* ===== GHIBLI CLOUDS ===== */
  .ghibli-cloud {
    position: absolute;
    width: 180px;
    height: 60px;
    animation: cloudDrift linear infinite;
    filter: blur(1px);
  }

  .cloud-shape {
    width: 100%;
    height: 100%;
    filter: drop-shadow(0 2px 4px rgba(168, 218, 220, 0.2));
  }

  @keyframes cloudDrift {
    0% {
      transform: translateX(-10vw);
    }
    100% {
      transform: translateX(110vw);
    }
  }

  /* ===== FLYING BIRDS ===== */
  .flying-bird {
    position: absolute;
    animation: birdFly linear infinite;
  }

  .bird-silhouette {
    animation: birdFlap 1.2s ease-in-out infinite;
  }

  @keyframes birdFly {
    0% {
      transform: translateX(-50px) translateY(0);
    }
    50% {
      transform: translateX(50vw) translateY(-30px);
    }
    100% {
      transform: translateX(calc(100vw + 50px)) translateY(0);
    }
  }

  @keyframes birdFlap {
    0%,
    100% {
      transform: scaleY(1);
    }
    50% {
      transform: scaleY(0.8);
    }
  }

  /* ===== NATURE PARTICLES ===== */
  .nature-particle {
    position: absolute;
    animation: floatDown linear infinite;
    opacity: 0;
  }

  @keyframes floatDown {
    0% {
      transform: translateY(-20px) translateX(0) rotate(0deg);
      opacity: 0;
    }
    10% {
      opacity: 0.7;
    }
    90% {
      opacity: 0.7;
    }
    100% {
      transform: translateY(100vh) translateX(50px) rotate(360deg);
      opacity: 0;
    }
  }

  /* ===== LIGHT RAYS ===== */
  .light-rays-container {
    position: absolute;
    inset: 0;
  }

  .sun-ray {
    position: absolute;
    top: -50%;
    width: 2px;
    height: 150%;
    background: linear-gradient(to bottom, transparent 0%, rgba(254, 250, 224, 0.8) 20%, transparent 40%);
    animation: rayPulse 8s ease-in-out infinite;
    transform-origin: top center;
  }

  @keyframes rayPulse {
    0%,
    100% {
      opacity: 0.3;
      transform: rotate(-2deg);
    }
    50% {
      opacity: 0.6;
      transform: rotate(2deg);
    }
  }

  /* ===== TEXTURES ===== */
  .watercolor-texture {
    position: fixed;
    inset: 0;
    background-image: radial-gradient(ellipse at 20% 30%, rgba(168, 218, 220, 0.03) 0%, transparent 50%), radial-gradient(ellipse at 80% 70%, rgba(254, 250, 224, 0.05) 0%, transparent 50%),
      radial-gradient(ellipse at 50% 50%, rgba(217, 228, 221, 0.02) 0%, transparent 60%);
    pointer-events: none;
    z-index: 1;
  }

  .paper-grain {
    position: fixed;
    inset: 0;
    background-image: url("https://www.transparenttextures.com/patterns/p6.png");
    opacity: 0.15;
    pointer-events: none;
    z-index: 1;
    mix-blend-mode: multiply;
  }

  /* ===== MAIN CONTENT ===== */
  .main-content {
    position: relative;
    z-index: 10;
  }

  /* ===== ARCHIVE SECTION ===== */
  .archive-section {
    position: relative;
    padding: 6rem 0 8rem;
    background: linear-gradient(to bottom, #fefae0 0%, #f8f6e8 50%, #f1f0e8 100%);
    border-top: 4px solid #2d2d2d;
    border-bottom: 4px solid #2d2d2d;
    overflow: hidden;
  }

  /* ===== NATURE SIDEBAR ===== */
  .nature-sidebar {
    position: absolute;
    top: 5rem;
    left: 1.5rem;
    display: none;
    flex-direction: column;
    gap: 2rem;
    opacity: 0.25;
    z-index: 5;
  }

  @media (min-width: 1280px) {
    .nature-sidebar {
      display: flex;
    }
  }

  .nature-icon {
    font-size: 3rem;
    animation: gentleFloat ease-in-out infinite;
    filter: drop-shadow(0 2px 4px rgba(96, 108, 56, 0.1));
  }

  @keyframes gentleFloat {
    0%,
    100% {
      transform: translateY(0) rotate(-5deg);
    }
    50% {
      transform: translateY(-15px) rotate(5deg);
    }
  }

  /* ===== GRASS DECORATION ===== */
  .grass-decoration {
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
    height: 100px;
    pointer-events: none;
    opacity: 0.15;
    z-index: 1;
  }

  .grass-blade {
    position: absolute;
    bottom: 0;
    width: 3px;
    background: linear-gradient(to top, #606c38, transparent);
    transform-origin: bottom center;
    animation: grassSway ease-in-out infinite;
  }

  @keyframes grassSway {
    0%,
    100% {
      transform: rotate(-3deg);
    }
    50% {
      transform: rotate(3deg);
    }
  }

  /* ===== ARCHIVE HEADER ===== */
  .archive-header {
    position: relative;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 2rem;
    margin-bottom: 5rem;
    padding: 3rem;
    background: linear-gradient(135deg, #fdf6e3 0%, #fefae0 100%);
    border: 4px solid #2d2d2d;
    box-shadow:
      12px 12px 0 rgba(188, 108, 37, 0.4),
      12px 12px 0 0 #bc6c25;
    border-radius: 2px;
  }

  @media (min-width: 768px) {
    .archive-header {
      flex-direction: row;
      justify-content: space-between;
      align-items: center;
    }
  }

  /* Watercolor Splash Behind Header */
  .watercolor-splash {
    position: absolute;
    inset: -20px;
    background: radial-gradient(ellipse at 30% 40%, rgba(168, 218, 220, 0.1) 0%, transparent 60%);
    filter: blur(30px);
    z-index: -1;
  }

  .header-content {
    flex: 1;
    text-align: center;
  }

  @media (min-width: 768px) {
    .header-content {
      text-align: left;
    }
  }

  .header-badge {
    display: inline-flex;
    align-items: center;
    gap: 0.5rem;
    background: #606c38;
    color: #fefae0;
    padding: 0.5rem 1.25rem;
    font-size: 0.875rem;
    text-transform: uppercase;
    letter-spacing: 0.2em;
    border-radius: 2px;
    margin-bottom: 1.5rem;
    box-shadow: 0 4px 8px rgba(40, 54, 24, 0.2);
  }

  .badge-dot {
    width: 6px;
    height: 6px;
    background: #fefae0;
    border-radius: 50%;
    animation: pulse 2s ease-in-out infinite;
  }

  .badge-sparkle {
    animation: sparkle 3s ease-in-out infinite;
  }

  @keyframes sparkle {
    0%,
    100% {
      opacity: 0.5;
      transform: scale(0.8);
    }
    50% {
      opacity: 1;
      transform: scale(1.2);
    }
  }

  /* ===== ARCHIVE TITLE ===== */
  .archive-title {
    position: relative;
    font-size: 4rem;
    font-weight: normal;
    text-transform: uppercase;
    line-height: 0.9;
    margin-bottom: 1rem;
    display: inline-block;
  }

  @media (min-width: 768px) {
    .archive-title {
      font-size: 5rem;
    }
  }

  .title-main {
    display: block;
    color: #2d2d2d;
    text-shadow:
      3px 3px 0 rgba(254, 250, 224, 0.5),
      -1px -1px 0 rgba(96, 108, 56, 0.1);
  }

  .title-accent {
    display: block;
    color: #bc6c25;
    font-style: italic;
    position: relative;
  }

  .title-underline {
    position: absolute;
    bottom: -8px;
    left: 0;
    right: 0;
    height: 6px;
    background: repeating-linear-gradient(90deg, #bc6c25 0px, #bc6c25 15px, transparent 15px, transparent 25px);
    opacity: 0.6;
  }

  /* ===== FILTER STATUS ===== */
  .filter-status {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 0.5rem;
    font-size: 1.5rem;
    color: #606c38;
    opacity: 0.85;
    text-transform: uppercase;
  }

  @media (min-width: 768px) {
    .filter-status {
      justify-content: flex-start;
    }
  }

  .status-icon {
    font-size: 1.25rem;
  }

  .status-value {
    color: #bc6c25;
    font-weight: bold;
  }

  .filter-container {
    margin-top: 2rem;
  }

  @media (min-width: 768px) {
    .filter-container {
      margin-top: 0;
    }
  }

  /* ===== GAME LIST ===== */
  .game-list-wrapper {
    position: relative;
    min-height: 400px;
  }

  /* ===== SECTION HILLS ===== */
  .section-hills {
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
    pointer-events: none;
    opacity: 0.6;
  }

  .hills-svg {
    width: 100%;
    height: auto;
    display: block;
  }

  /* ===== SHOWCASE SECTION ===== */
  .showcase-section {
    position: relative;
    padding: 5rem 0;
    background: linear-gradient(to bottom, #fefae0 0%, #f1f0e8 100%);
    overflow: hidden;
  }

  /* ===== DANDELION SEEDS ===== */
  .dandelion-seed {
    position: absolute;
    animation: seedFloat 20s ease-in-out infinite;
    opacity: 0;
  }

  @keyframes seedFloat {
    0% {
      transform: translateY(-20px) translateX(0) rotate(0deg);
      opacity: 0;
    }
    10% {
      opacity: 0.6;
    }
    90% {
      opacity: 0.6;
    }
    100% {
      transform: translateY(100vh) translateX(30px) rotate(180deg);
      opacity: 0;
    }
  }

  /* ===== ATMOSPHERIC EFFECTS ===== */
  .atmospheric-vignette {
    position: fixed;
    inset: 0;
    pointer-events: none;
    box-shadow: inset 0 0 200px rgba(96, 108, 56, 0.12);
    z-index: 100;
  }

  .wind-overlay {
    position: fixed;
    inset: 0;
    background: linear-gradient(90deg, transparent 0%, rgba(168, 218, 220, 0.03) 50%, transparent 100%);
    animation: windBlow 15s linear infinite;
    pointer-events: none;
    z-index: 2;
  }

  @keyframes windBlow {
    0% {
      transform: translateX(-100%);
    }
    100% {
      transform: translateX(100%);
    }
  }

  /* ===== MISC ANIMATIONS ===== */
  @keyframes pulse {
    0%,
    100% {
      opacity: 1;
    }
    50% {
      opacity: 0.5;
    }
  }

  /* ===== PIXEL ART PRESERVATION ===== */
  :global(img) {
    image-rendering: pixelated;
  }
</style>
