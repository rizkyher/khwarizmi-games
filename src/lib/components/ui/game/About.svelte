<script lang="ts">
  import { Wind, BookOpen, Map, Sparkles, Ghost } from "@lucide/svelte";

  // Svelte 5 State
  let isHovered = $state(false);
  let mousePos = $state({ x: 0, y: 0 });

  // Menggunakan innerWidth untuk memastikan safety SSR seperti sebelumnya
  let innerWidth = $state(0);

  function handleMouseMove(e: MouseEvent) {
    const rect = (e.currentTarget as HTMLElement).getBoundingClientRect();
    // Normalisasi posisi mouse -0.5 sampai 0.5
    mousePos.x = (e.clientX - rect.left) / rect.width - 0.5;
    mousePos.y = (e.clientY - rect.top) / rect.height - 0.5;
  }
</script>

<svelte:window bind:innerWidth />

<section id="about-us" class="relative py-24 bg-[#fdf6e3] overflow-hidden border-b-4 border-[#2d2d2d]" onmousemove={handleMouseMove} onmouseenter={() => (isHovered = true)} onmouseleave={() => (isHovered = false)} role="region">
  <div class="absolute inset-0 pointer-events-none overflow-hidden">
    <div class="absolute inset-0 opacity-[0.03] bg-[url('https://www.transparenttextures.com/patterns/p6.png')]"></div>

    <div class="absolute top-20 left-10 text-8xl opacity-10 transition-transform duration-1000 ease-out animate-float-slow" style="transform: translate({mousePos.x * -60}px, {mousePos.y * -60}px) rotate({12 + mousePos.x * 20}deg);">🌿</div>
    <div class="absolute top-1/2 right-[5%] text-7xl opacity-5 animate-bounce-slow" style="transform: translate({mousePos.x * 40}px, {mousePos.y * -20}px);">🍃</div>
    <div class="absolute bottom-10 left-1/4 text-9xl opacity-10 transition-transform duration-1000 ease-out" style="transform: translate({mousePos.x * 30}px, {mousePos.y * 50}px) rotate({mousePos.x * -15}deg);">🍄</div>
  </div>

  <div class="container mx-auto px-6 max-w-6xl relative z-10">
    <div class="grid grid-cols-1 lg:grid-cols-2 gap-16 items-center">
      <div class="relative group">
        <div class="absolute inset-4 bg-[#2d2d2d] translate-x-4 translate-y-4 rounded-sm transition-transform duration-500 group-hover:translate-x-8 group-hover:translate-y-8"></div>

        <div class="relative aspect-square bg-white border-4 border-[#2d2d2d] overflow-hidden group-hover:-translate-x-2 group-hover:-translate-y-2 transition-transform duration-500 shadow-inner">
          <div class="absolute inset-0 bg-[#d9e4dd] flex items-center justify-center overflow-hidden">
            <div class="absolute inset-0 bg-[radial-gradient(circle_at_50%_120%,#bc6c2520_0%,transparent_70%)]"></div>

            <div class="relative text-center space-y-4 z-10">
              <div class="text-[10rem] md:text-[12rem] animate-float drop-shadow-xl select-none">🏡</div>
              <div class="font-pixel text-2xl text-[#606c38] tracking-widest flex items-center justify-center gap-3">
                <span class="inline-block w-2 h-2 bg-[#606c38] animate-ping"></span>
                Entering Khwarizmi Hub...
              </div>
            </div>

            <div class="absolute top-10 left-10 text-2xl animate-bounce-slow opacity-40">✨</div>
            <div class="absolute bottom-20 right-10 text-3xl animate-float opacity-30" style="animation-delay: 1s">✨</div>
          </div>

          <div class="absolute inset-0 bg-gradient-to-tr from-[#606c38]/10 via-transparent to-white/20 pointer-events-none"></div>

          <div class="absolute bottom-6 left-6 bg-white border-2 border-[#2d2d2d] px-4 py-2 shadow-[4px_4px_0px_#2d2d2d] group-hover:scale-105 transition-transform">
            <span class="font-pixel text-lg text-[#2d2d2d] flex items-center gap-2">
              <Map size={18} class="text-[#bc6c25]" /> COORDINATE: 07°S, 110°E
            </span>
          </div>
        </div>
      </div>

      <div class="space-y-8">
        <div class="space-y-4">
          <div
            class="inline-flex items-center gap-2 px-4 py-1.5 bg-[#606c38] text-white font-pixel text-sm uppercase tracking-[0.2em] border-2 border-[#2d2d2d] shadow-[4px_4px_0px_#2d2d2d] hover:translate-x-1 hover:translate-y-1 hover:shadow-none transition-all cursor-default"
          >
            <BookOpen size={14} />
            Our Journey
          </div>

          <h2 class="font-pixel text-6xl md:text-8xl text-[#2d2d2d] leading-[0.85] uppercase tracking-tighter">
            Where Pixels Find <br />
            <span class="text-[#bc6c25] italic relative inline-block">
              Their Soul
              <svg class="absolute -bottom-2 left-0 w-full h-3 text-[#606c38]/30" viewBox="0 0 100 10" preserveAspectRatio="none">
                <path d="M0 5 Q 25 0 50 5 T 100 5" fill="none" stroke="currentColor" stroke-width="4" />
              </svg>
            </span>.
          </h2>
        </div>

        <div class="space-y-6 font-pixel text-2xl md:text-3xl text-[#5d4037] leading-tight">
          <p class="opacity-90">
            Di balik rimbunnya hutan digital Khwarizmi, kami percaya bahwa teknologi bukan hanya barisan kode dingin. Ia adalah <span class="text-[#606c38] font-bold underline decoration-dotted">kuas</span>, dan layar adalah kanvasnya.
          </p>

          <div class="relative group/quote">
            <div class="absolute -left-2 top-0 w-1 h-full bg-[#606c38] scale-y-0 group-hover/quote:scale-y-100 transition-transform origin-top duration-500"></div>
            <p class="pl-6 italic bg-[#606c38]/5 py-6 border-l-4 border-[#606c38]/20 group-hover/quote:bg-[#606c38]/10 transition-colors">
              "Kami merajut kenangan masa kecil yang hangat dengan ketajaman estetika pixel modern, menciptakan tempat peristirahatan bagi imajinasi Anda."
            </p>
          </div>
        </div>

        <div class="grid grid-cols-2 gap-6">
          <div class="group/stat bg-white border-3 border-[#2d2d2d] p-6 shadow-[6px_6px_0px_#2d2d2d] hover:-translate-y-2 hover:shadow-[8px_8px_0px_#bc6c25] transition-all duration-300">
            <div class="text-[#bc6c25] text-5xl font-pixel leading-none group-hover/stat:scale-110 transition-transform origin-left">12+</div>
            <div class="text-[#606c38] text-xl font-pixel uppercase tracking-tight mt-1">Worlds Created</div>
          </div>

          <div class="group/stat bg-white border-3 border-[#2d2d2d] p-6 shadow-[6px_6px_0px_#2d2d2d] hover:-translate-y-2 hover:shadow-[8px_8px_0px_#606c38] transition-all duration-300">
            <div class="text-[#bc6c25] text-5xl font-pixel leading-none group-hover/stat:scale-110 transition-transform origin-left">100%</div>
            <div class="text-[#606c38] text-xl font-pixel uppercase tracking-tight mt-1">Hand-Crafted</div>
          </div>
        </div>

        <button class="group relative inline-flex items-center gap-4 px-10 py-5 bg-[#2d2d2d] text-white font-pixel text-3xl uppercase tracking-widest transition-all hover:bg-[#3d4c53] active:translate-y-1">
          <span class="relative z-10">Explore Our Lore</span>
          <Sparkles class="relative z-10 transition-all group-hover:rotate-12 group-hover:scale-125 text-[#bc6c25]" />

          <div class="absolute inset-0 bg-[#bc6c25] scale-x-0 group-hover:scale-x-100 transition-transform origin-left duration-500 z-0"></div>

          <div class="absolute right-4 opacity-0 group-hover:opacity-100 group-hover:right-2 transition-all z-10 text-white">→</div>
        </button>
      </div>
    </div>
  </div>

  <div class="absolute bottom-0 left-0 w-full h-24 bg-gradient-to-t from-[#606c38]/10 to-transparent pointer-events-none"></div>
</section>

<style>
  @import url("https://fonts.googleapis.com/css2?family=VT323&display=swap");

  .font-pixel {
    font-family: "VT323", monospace;
  }

  /* Animasi Khusus */
  @keyframes float {
    0%,
    100% {
      transform: translateY(0) rotate(0deg);
    }
    50% {
      transform: translateY(-20px) rotate(5deg);
    }
  }

  @keyframes float-slow {
    0%,
    100% {
      transform: translateY(0) translateX(0);
    }
    50% {
      transform: translateY(-10px) translateX(10px);
    }
  }

  @keyframes bounce-slow {
    0%,
    100% {
      transform: translateY(0);
    }
    50% {
      transform: translateY(-15px);
    }
  }

  .animate-float {
    animation: float 5s ease-in-out infinite;
  }

  .animate-float-slow {
    animation: float-slow 8s ease-in-out infinite;
  }

  .animate-bounce-slow {
    animation: bounce-slow 4s ease-in-out infinite;
  }

  section {
    image-rendering: pixelated;
  }
</style>
