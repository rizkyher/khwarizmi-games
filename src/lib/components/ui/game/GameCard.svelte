<script lang="ts">
  import { MapPin, Sparkles, ArrowUpRight } from "@lucide/svelte";

  // Svelte 5 Props
  let { game, onOpenPreview } = $props();
</script>

<div class="group relative h-full p-2 w-full transition-all duration-300">
  <div class="absolute inset-0 bg-[#3e2723]/10 translate-x-4 translate-y-4 rounded-xl group-hover:translate-x-2 group-hover:translate-y-2 transition-all duration-300" aria-hidden="true"></div>

  <button
    type="button"
    onclick={() => onOpenPreview(game)}
    class="relative w-full h-full text-left bg-[#fdfaf1] border-[3px] border-[#3e2723] rounded-xl p-3
           overflow-hidden transition-all duration-500 group-hover:-translate-y-1
           focus:outline-none focus:ring-4 focus:ring-[#606c38]/30 active:scale-[0.98]"
  >
    <div class="relative aspect-4/3 rounded-lg overflow-hidden border-2 border-[#3e2723] mb-4 bg-[#d9e4dd] group">
      <img src={game.img} alt={game.title} class="size-full object-cover pixelated transition-transform duration-700 ease-out group-hover:scale-110 group-hover:rotate-1" />

      <div class="absolute inset-0 bg-linear-to-t from-[#3e2723]/20 to-transparent opacity-0 group-hover:opacity-100 transition-opacity"></div>

      <div class="absolute top-2 left-2 flex items-center gap-1.5 bg-[#fdfaf1] border-2 border-[#3e2723] px-3 py-0.5 rounded-full shadow-[2px_2px_0px_#3e2723]">
        <Sparkles size={10} class="text-[#606c38]" />
        <span class="font-['VT323'] text-[#3e2723] text-sm uppercase">{game.category}</span>
      </div>

      <div class="absolute bottom-2 right-2 size-8 bg-[#606c38] text-white border-2 border-[#3e2723] flex items-center justify-center translate-y-12 group-hover:translate-y-0 transition-transform duration-300">
        <ArrowUpRight size={16} />
      </div>
    </div>

    <div class="space-y-2">
      <div class="relative">
        <h3 class="font-['VT323'] text-3xl text-[#3e2723] leading-none uppercase group-hover:text-[#bc6c25] transition-colors">
          {game.title}
        </h3>
        <div class="h-1 w-0 bg-[#bc6c25]/30 group-hover:w-full transition-all duration-500 mt-1"></div>
      </div>

      <div class="flex justify-between items-center pt-1">
        <div class="flex items-center gap-1.5">
          <MapPin size={14} class="text-[#606c38]" />
          <p class="font-['VT323'] text-[#5d4037]/80 text-lg uppercase tracking-tight">
            {game.developer}
          </p>
        </div>

        <div class="flex items-center gap-2">
          <span class="font-['VT323'] text-xs text-[#606c38] opacity-0 group-hover:opacity-100 transition-opacity uppercase">Playable</span>
          <div class="size-2 rounded-full bg-[#606c38] shadow-[0_0_8px_#606c38]"></div>
        </div>
      </div>
    </div>

    <div class="absolute inset-0 pointer-events-none opacity-[0.03] mix-blend-multiply bg-[url('https://www.transparenttextures.com/patterns/stardust.png')]"></div>
  </button>
</div>

<style>
  .pixelated {
    image-rendering: pixelated;
    image-rendering: crisp-edges;
  }

  /* Animasi halus untuk tombol saat ditekan */
  button:active {
    box-shadow: none;
    transform: translateY(2px) translateX(2px);
  }
</style>
