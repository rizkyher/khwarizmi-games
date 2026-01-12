<script lang="ts">
  import { Play, Sparkles, Wind } from "@lucide/svelte";
  import { Button } from "$lib/components/ui/button";

  // STATE
  let innerWidth = $state(0);
  let innerHeight = $state(0);
  let mouseX = $state(0);
  let mouseY = $state(0);

  function handleMouseMove(e: MouseEvent) {
    if (innerWidth > 0 && innerHeight > 0) {
      // Mouse interaction physics
      mouseX = (e.clientX / innerWidth - 0.5) * 30;
      mouseY = (e.clientY / innerHeight - 0.5) * 30;
    }
  }
</script>

<svelte:window bind:innerWidth bind:innerHeight />

<section onmousemove={handleMouseMove} role="region" class="relative min-h-screen w-full flex flex-col items-center justify-center overflow-hidden bg-[#e0f2f1] cursor-default selection:bg-[#bc6c25]/30 selection:text-[#2d2d2d]">
  <div class="fixed inset-0 pointer-events-none z-50 opacity-[0.05] mix-blend-multiply bg-[url('https://grainy-gradients.vercel.app/noise.svg')]"></div>

  <div class="absolute inset-0 bg-gradient-to-b from-[#A5D8FF] via-[#E8F5E9] to-[#FFF9C4]">
    <div class="absolute -top-[50%] -left-[20%] w-[150%] h-[150%] bg-[conic-gradient(from_0deg,transparent_0deg,white_10deg,transparent_20deg,white_40deg,transparent_60deg)] opacity-10 animate-spin-slow pointer-events-none"></div>

    <div class="pixel-cloud absolute top-[15%] left-[-5%] opacity-70 scale-150 animate-drift-slow" style="transform: translate({mouseX * 0.2}px, {mouseY * 0.1}px)">☁️</div>
    <div class="pixel-cloud absolute top-[40%] right-[-5%] opacity-50 scale-125 animate-drift-medium" style="transform: translate({mouseX * -0.3}px, {mouseY * 0.2}px)">☁️</div>
    <div class="pixel-cloud absolute top-[10%] right-[20%] opacity-40 animate-drift-fast" style="transform: translate({mouseX * 0.1}px, {mouseY * 0.4}px)">☁️</div>
  </div>

  {#each Array(25) as _, i}
    <div
      class="absolute rounded-full animate-float-particle"
      style="
        left: {Math.random() * 100}%; 
        top: {Math.random() * 100}%; 
        width: {Math.random() * 6 + 2}px;
        height: {Math.random() * 6 + 2}px;
        background-color: {Math.random() > 0.6 ? '#2d2d2d' : '#ffffff'};
        opacity: {Math.random() * 0.5 + 0.2};
        /* Randomize animation duration for chaotic feel */
        animation-duration: {Math.random() * 15 + 10}s;
        animation-delay: {Math.random() * -10}s;
      "
    ></div>
  {/each}

  <div class="relative z-20 flex flex-col items-center text-center px-4 max-w-4xl">
    <div class="mb-8 px-4 py-1 bg-[#fdf6e3]/90 border-2 border-[#2d2d2d] shadow-[4px_4px_0px_0px_rgba(45,45,45,0.2)] animate-float">
      <span class="text-[10px] md:text-xs font-mono font-bold text-[#606c38] flex items-center gap-2 tracking-[0.2em]">
        <Sparkles size={12} class="animate-pulse text-[#bc6c25]" />
        EST. 2024 // SPIRIT_REALM
      </span>
    </div>

    <div class="relative group">
      <h1 class="font-pixel text-6xl md:text-9xl text-[#2d2d2d] leading-none select-none drop-shadow-sm z-10 relative">
        <span class="block" style="text-shadow: 4px 4px 0px #fdf6e3;">KHWARIZMI</span>
        <span class="block text-[#556b2f] italic mt-[-10px] md:mt-[-25px]" style="text-shadow: 3px 3px 0px #fdf6e3;">Games</span>
      </h1>

      <div class="absolute top-0 right-0 text-5xl pointer-events-none animate-fly-path z-50">
        <div class="animate-flutter">🦋</div>
      </div>

      <div class="absolute bottom-0 left-10 text-3xl pointer-events-none animate-fly-path-reverse z-0 opacity-80">
        <div class="animate-flutter delay-100">🦋</div>
      </div>
    </div>

    <p class="mt-8 max-w-lg font-mono text-[#4a4036] text-lg md:text-xl leading-relaxed bg-[#fdf6e3]/60 backdrop-blur-sm p-6 rounded-sm border-2 border-[#2d2d2d]/10 shadow-sm relative overflow-hidden">
      <span class="absolute top-0 left-[-100%] w-[50%] h-full bg-gradient-to-r from-transparent via-white/40 to-transparent animate-shimmer skew-x-12"></span>
      A digital archive where <span class="text-[#bc6c25] font-bold border-b-2 border-[#bc6c25]/30">imagination</span> meets the warmth of watercolor and pixel craftsmanship.
    </p>

    <div class="mt-12 flex flex-col items-center gap-6">
      <Button
        class="group relative h-14 px-10 bg-[#2d2d2d] hover:bg-[#3d4c53] text-[#fdf6e3] border-b-4 border-r-4 border-[#bc6c25] active:border-0 active:translate-y-1 transition-all rounded-none font-pixel text-xl tracking-wide overflow-hidden"
      >
        <Play size={18} class="mr-3 fill-current group-hover:rotate-12 transition-transform" />
        <span class="relative z-10">ENTER_PARK</span>
        <div class="absolute inset-0 bg-[#556b2f] transform translate-y-full group-hover:translate-y-0 transition-transform duration-300 ease-out z-0"></div>
      </Button>

      <div class="flex items-center gap-2 text-[#606c38] font-mono text-xs opacity-80 animate-pulse">
        <Wind size={14} />
        <span>Breathe in, breathe out.</span>
      </div>
    </div>
  </div>

  <div class="absolute bottom-0 w-full h-48 pointer-events-none z-10">
    <div class="absolute bottom-0 w-full h-full bg-[#C5E1A5] opacity-80 clip-hills-far transition-transform duration-75" style="transform: translateX({mouseX * 0.05}px)"></div>
    <div class="absolute bottom-0 w-full h-40 bg-[#AED581] opacity-90 clip-hills-mid transition-transform duration-75" style="transform: translateX({mouseX * 0.1}px)"></div>

    <!-- <div class="absolute bottom-0 w-full h-24 bg-[#558B2F] border-t-4 border-[#2d2d2d]">
      <div class="absolute inset-0 opacity-10 bg-[radial-gradient(#000_1px,transparent_1px)] [background-size:16px_16px]"></div>

      <div class="flex justify-between items-end h-full px-2 w-[110%] -ml-[5%] overflow-hidden">
        {#each Array(45) as _, i}
          <div
            class="text-2xl relative animate-sway-grass"
            style="
                /* Randomize start time and speed for natural wind effect */
                animation-delay: {i * 0.1 - 5}s; 
                animation-duration: {3 + Math.random() * 3}s;
                transform-origin: bottom center; 
                bottom: -6px;
                filter: hue-rotate({i * 5}deg) brightness({0.9 + Math.random() * 0.2});
                font-size: {Math.random() * 15 + 20}px;
                opacity: 0.9;
                z-index: {i % 2 === 0 ? 10 : 0};
              "
          >
            🌱
          </div>
        {/each}
      </div>
    </div> -->
  </div>
</section>

<style>
  @import url("https://fonts.googleapis.com/css2?family=VT323&display=swap");

  :global(body) {
    margin: 0;
    padding: 0;
    background: #fdf6e3;
  }

  .font-pixel {
    font-family: "VT323", monospace;
  }

  /* --- Clip Paths --- */
  .clip-hills-far {
    clip-path: polygon(0% 100%, 0% 30%, 20% 50%, 40% 20%, 60% 45%, 80% 25%, 100% 40%, 100% 100%);
  }
  .clip-hills-mid {
    clip-path: polygon(0% 100%, 0% 60%, 15% 45%, 35% 70%, 55% 50%, 75% 65%, 100% 55%, 100% 100%);
  }

  /* --- Cloud Styles --- */
  .pixel-cloud {
    font-size: 8rem;
    filter: sepia(0.3) hue-rotate(180deg) opacity(0.8);
    user-select: none;
    will-change: transform;
  }

  /* --- Complex Animations --- */

  /* 1. Kupu-kupu terbang meliuk (Path) */
  @keyframes flyPath {
    0% {
      transform: translate(0, 0) rotate(0deg);
    }
    25% {
      transform: translate(60px, -40px) rotate(10deg);
    }
    50% {
      transform: translate(20px, -80px) rotate(-5deg);
    }
    75% {
      transform: translate(-40px, -30px) rotate(-15deg);
    }
    100% {
      transform: translate(0, 0) rotate(0deg);
    }
  }

  @keyframes flyPathReverse {
    0% {
      transform: translate(0, 0) rotate(0deg) scaleX(-1);
    }
    33% {
      transform: translate(-50px, -30px) rotate(-10deg) scaleX(-1);
    }
    66% {
      transform: translate(30px, -60px) rotate(5deg) scaleX(-1);
    }
    100% {
      transform: translate(0, 0) rotate(0deg) scaleX(-1);
    }
  }

  .animate-fly-path {
    animation: flyPath 12s ease-in-out infinite;
  }
  .animate-fly-path-reverse {
    animation: flyPathReverse 15s ease-in-out infinite;
  }

  /* Gerakan sayap kupu-kupu */
  @keyframes flutter {
    0%,
    100% {
      transform: scaleY(1);
    }
    50% {
      transform: scaleY(0.8);
    }
  }
  .animate-flutter {
    animation: flutter 0.2s linear infinite;
  }

  /* 2. Rumput Bergoyang (Wind) */
  @keyframes swayGrass {
    0%,
    100% {
      transform: rotate(-6deg);
    }
    50% {
      transform: rotate(8deg);
    }
  }
  .animate-sway-grass {
    will-change: transform;
  } /* Performance optimization */

  /* 3. Awan Berarak (Drift) */
  @keyframes drift {
    0% {
      transform: translateX(0);
    }
    50% {
      transform: translateX(20px);
    }
    100% {
      transform: translateX(0);
    }
  }
  .animate-drift-slow {
    animation: drift 20s ease-in-out infinite;
  }
  .animate-drift-medium {
    animation: drift 15s ease-in-out infinite reverse;
  }
  .animate-drift-fast {
    animation: drift 12s ease-in-out infinite;
  }

  /* 4. Partikel Roh (Float) */
  @keyframes floatParticle {
    0% {
      transform: translateY(0) scale(1);
      opacity: 0;
    }
    20% {
      opacity: 0.6;
    }
    80% {
      opacity: 0.6;
    }
    100% {
      transform: translateY(-100px) scale(0);
      opacity: 0;
    }
  }
  .animate-float-particle {
    animation-name: floatParticle;
    animation-timing-function: linear;
    animation-iteration-count: infinite;
  }

  /* 5. Utility Animations */
  @keyframes spin {
    from {
      transform: rotate(0deg);
    }
    to {
      transform: rotate(360deg);
    }
  }
  .animate-spin-slow {
    animation: spin 60s linear infinite;
  }

  @keyframes shimmer {
    from {
      left: -100%;
    }
    to {
      left: 200%;
    }
  }
  .animate-shimmer {
    animation: shimmer 4s infinite;
  }

  @keyframes float {
    0%,
    100% {
      transform: translateY(0);
    }
    50% {
      transform: translateY(-5px);
    }
  }
  .animate-float {
    animation: float 4s ease-in-out infinite;
  }
</style>
