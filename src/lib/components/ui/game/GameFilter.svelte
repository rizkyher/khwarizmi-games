<script lang="ts">
  import { fade } from "svelte/transition";

  let { selected = $bindable() } = $props();
  const categories = ["All Games", "Action", "RPG", "Experimental", "Web3"];
</script>

<div class="flex flex-wrap items-center justify-center lg:justify-start gap-4 p-1">
  {#each categories as cat}
    <button onclick={() => (selected = cat)} class="relative px-6 py-2 group transition-all duration-300">
      <div
        class="absolute inset-0 rounded-full border transition-all duration-300
        {selected === cat ? 'bg-[#606c38] border-[#606c38] shadow-lg shadow-[#606c38]/20' : 'bg-white/50 border-[#8b5a2b]/10 group-hover:bg-white group-hover:border-[#606c38]/30'}"
      ></div>

      <span
        class="relative z-10 font-['VT323'] text-xl uppercase tracking-widest transition-colors duration-300
        {selected === cat ? 'text-[#f1f0e8]' : 'text-[#5d4037]/60 group-hover:text-[#2d2d2d]'}"
      >
        {cat.replace(" ", "_")}
      </span>

      {#if selected === cat}
        <span in:fade class="absolute -top-1 -right-1 text-sm animate-bounce"> ✨ </span>
      {/if}
    </button>
  {/each}
</div>
