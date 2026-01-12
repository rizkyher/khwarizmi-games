<script lang="ts">
  import { Wind, BookOpen, Map, Sparkles } from "@lucide/svelte";
  import { onMount } from "svelte";

  // Svelte 5 State untuk interaksi ringan
  let isHovered = $state(false);
  let mousePos = $state({ x: 0, y: 0 });

  function handleMouseMove(e: MouseEvent) {
    const rect = (e.currentTarget as HTMLElement).getBoundingClientRect();
    mousePos.x = (e.clientX - rect.left) / rect.width - 0.5;
    mousePos.y = (e.clientY - rect.top) / rect.height - 0.5;
  }
</script>

<section id="about-us" class="relative py-24 bg-[#fdf6e3] overflow-hidden border-b-4 border-[#2d2d2d]" onmousemove={handleMouseMove} onmouseenter={() => (isHovered = true)} onmouseleave={() => (isHovered = false)} role="region">
  <div class="absolute inset-0 pointer-events-none overflow-hidden">
    <div class="absolute inset-0 opacity-[0.03] bg-[url('https://www.transparenttextures.com/patterns/p6.png')]"></div>

    <div class="absolute top-20 left-10 text-8xl opacity-5 transition-transform duration-700 ease-out" style="transform: translate({mousePos.x * -40}px, {mousePos.y * -40}px) rotate(12deg);">🌿</div>
    <div class="absolute bottom-10 right-10 text-9xl opacity-5 transition-transform duration-700 ease-out" style="transform: translate({mousePos.x * 30}px, {mousePos.y * 30}px) rotate(-15deg);">🍄</div>
  </div>

  <div class="container mx-auto px-6 max-w-6xl relative z-10">
    <div class="grid grid-cols-1 lg:grid-cols-2 gap-16 items-center">
      <div class="relative group">
        <div class="absolute inset-4 bg-[#2d2d2d] translate-x-4 translate-y-4 rounded-sm transition-transform group-hover:translate-x-6 group-hover:translate-y-6"></div>

        <div class="relative aspect-square md:aspect-video lg:aspect-square bg-white border-4 border-[#2d2d2d] overflow-hidden group-hover:-translate-x-2 group-hover:-translate-y-2 transition-transform duration-500">
          <div class="absolute inset-0 bg-[#d9e4dd] flex items-center justify-center">
            <div class="text-center space-y-4">
              <div class="text-[12rem] animate-bounce select-none">🏡</div>
              <div class="font-['VT323'] text-2xl text-[#606c38] animate-pulse uppercase tracking-widest">Entering Khwarizmi Hub...</div>
            </div>
          </div>

          <div class="absolute inset-0 bg-linear-to-tr from-[#606c38]/20 via-transparent to-[#bc6c25]/10 pointer-events-none"></div>

          <div class="absolute bottom-6 left-6 bg-white border-2 border-[#2d2d2d] px-4 py-2 shadow-[4px_4px_0px_#2d2d2d]">
            <span class="font-['VT323'] text-lg text-[#2d2d2d] flex items-center gap-2">
              <Map size={18} /> COORDINATE: 07°S, 110°E
            </span>
          </div>
        </div>
      </div>

      <div class="space-y-8">
        <div class="space-y-4">
          <div class="inline-flex items-center gap-2 px-3 py-1 bg-[#606c38] text-white font-['VT323'] text-sm uppercase tracking-widest border-2 border-[#2d2d2d] shadow-[4px_4px_0px_#2d2d2d]">
            <BookOpen size={14} />
            Our Journey
          </div>

          <h2 class="font-['VT323'] text-5xl md:text-7xl text-[#2d2d2d] leading-[0.9] uppercase tracking-tighter">
            Where Pixels Find <span class="text-[#bc6c25] italic">Their Soul</span>.
          </h2>
        </div>

        <div class="space-y-6 font-['VT323'] text-xl md:text-2xl text-[#5d4037] leading-tight">
          <p>Di balik rimbunnya hutan digital Khwarizmi, kami percaya bahwa teknologi bukan hanya barisan kode dingin. Ia adalah kuas, dan layar adalah kanvasnya.</p>
          <p class="border-l-4 border-[#606c38] pl-6 italic bg-[#606c38]/5 py-4">"Kami merajut kenangan masa kecil yang hangat dengan ketajaman estetika pixel modern, menciptakan tempat peristirahatan bagi imajinasi Anda."</p>
        </div>

        <div class="grid grid-cols-2 gap-4">
          <div class="bg-white border-3 border-[#2d2d2d] p-4 shadow-[4px_4px_0px_#2d2d2d] hover:-translate-y-1 transition-transform">
            <div class="text-[#bc6c25] text-4xl font-['VT323'] leading-none">12+</div>
            <div class="text-[#606c38] text-lg font-['VT323'] uppercase tracking-tight">Worlds Created</div>
          </div>
          <div class="bg-white border-3 border-[#2d2d2d] p-4 shadow-[4px_4px_0px_#2d2d2d] hover:-translate-y-1 transition-transform">
            <div class="text-[#bc6c25] text-4xl font-['VT323'] leading-none">100%</div>
            <div class="text-[#606c38] text-lg font-['VT323'] uppercase tracking-tight">Hand-Crafted</div>
          </div>
        </div>

        <button class="group relative inline-flex items-center gap-3 px-8 py-4 bg-[#2d2d2d] text-white font-['VT323'] text-2xl uppercase tracking-widest transition-all hover:pr-12">
          Explore Our Lore
          <Sparkles class="transition-all group-hover:rotate-12" />
          <div class="absolute right-4 opacity-0 group-hover:opacity-100 group-hover:right-3 transition-all">→</div>
        </button>
      </div>
    </div>
  </div>

  <div class="absolute bottom-0 left-0 w-full h-12 bg-linear-to-t from-[#606c38]/10 to-transparent pointer-events-none"></div>
</section>

<style>
  /* Pixel-art rendering fix */
  section {
    image-rendering: pixelated;
  }
</style>
