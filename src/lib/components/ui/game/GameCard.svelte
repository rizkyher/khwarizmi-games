<script lang="ts">
  import { MapPin, Sparkles } from "@lucide/svelte";

  // Svelte 5 Props
  let { game, onOpenPreview } = $props();
</script>

<div class="group relative h-full p-3 w-full transition-all duration-300">
  <div class="absolute inset-0 bg-[#4a3b28]/20 translate-x-3 translate-y-3 rounded-4xl blur-sm group-hover:bg-[#4a3b28]/30 transition-all" aria-hidden="true"></div>

  <button
    type="button"
    onclick={() => onOpenPreview(game)}
    class="relative w-full h-full text-left bg-[#fdfaf1] border-[3px] border-[#3e2723] rounded-4xl p-4
           overflow-hidden transition-all duration-500 hover:-translate-y-2 hover:shadow-[0_20px_40px_rgba(0,0,0,0.1)]
           focus:outline-none focus:ring-4 focus:ring-[#8c9440] active:scale-95"
  >
    <div class="relative aspect-4/3 rounded-3xl overflow-hidden border-2 border-[#3e2723] mb-5 bg-[#e8e4d9]">
      <img src={game.img} alt={game.title} class="size-full object-cover pixelated group-hover:scale-105 transition-transform duration-1000 ease-out" />

      <div class="absolute top-3 left-3 flex items-center gap-1.5 bg-[#fdfaf1]/90 backdrop-blur-md border-2 border-[#3e2723] px-3 py-1 rounded-full shadow-sm">
        <Sparkles size={12} class="text-[#8c9440]" />
        <span class="font-['VT323'] text-[#3e2723] text-sm uppercase tracking-wider">{game.category}</span>
      </div>
    </div>

    <div class="space-y-3 px-1">
      <div class="flex items-center gap-2">
        <h3 class="font-['VT323'] text-3xl text-[#3e2723] leading-none uppercase">{game.title}</h3>
      </div>

      <div class="flex justify-between items-center border-t border-[#3e2723]/10 pt-3">
        <div class="flex items-center gap-1.5">
          <MapPin size={14} class="text-[#8c9440]" />
          <p class="font-['VT323'] text-[#5d4037] text-lg uppercase tracking-tight">{game.developer}</p>
        </div>
        <div class="size-2 rounded-full bg-[#8c9440] animate-pulse"></div>
      </div>
    </div>
  </button>
</div>

<style>
  .pixelated {
    image-rendering: pixelated;
    image-rendering: crisp-edges;
  }
</style>
