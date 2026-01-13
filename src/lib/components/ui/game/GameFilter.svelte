<script lang="ts">
  import { fade, scale } from "svelte/transition";

  let { selected = $bindable() } = $props();
  const categories = ["All Games", "Action", "RPG", "Experimental", "Web3"];
</script>

<div class="flex flex-wrap items-center justify-center lg:justify-start gap-3 p-2">
  {#each categories as cat}
    <button 
      onclick={() => (selected = cat)} 
      class="relative px-6 py-2 group transition-all duration-300"
    >
      <div
        class="absolute inset-0 transition-all duration-300 transform
        {selected === cat 
          ? 'bg-[#606c38] border-2 border-[#2d2d2d] rotate-1 shadow-[4px_4px_0px_#bc6c25]' 
          : 'bg-[#fefae0]/80 border-2 border-transparent group-hover:border-[#606c38]/30 group-hover:-rotate-1'}"
      ></div>

      <span
        class="relative z-10 font-['VT323'] text-2xl uppercase tracking-wider transition-colors duration-300
        {selected === cat ? 'text-[#fefae0]' : 'text-[#5d4037]/70 group-hover:text-[#2d2d2d]'}"
      >
        {cat.replace(" ", "_")}
      </span>

      {#if selected === cat}
        <div 
          in:scale={{ duration: 300, start: 0.5 }} 
          class="absolute -top-3 -right-2 z-20"
        >
          <span class="text-lg animate-pulse">✨</span>
        </div>
        
        <div 
          in:fade 
          class="absolute inset-0 bg-[#606c38]/10 blur-xl -z-10 scale-150"
        ></div>
      {/if}

      {#if selected !== cat}
        <span class="absolute -bottom-1 left-1/2 -translate-x-1/2 opacity-0 group-hover:opacity-100 group-hover:-bottom-2 transition-all text-xs">
          🍃
        </span>
      {/if}
    </button>
  {/each}
</div>

<style>
  button {
    cursor: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="m12 19 7-7 3 3-7 7-3-3Z"></path><path d="m18 13-1.5-7.5L2 2l3.5 14.5L13 18l5-5Z"></path><path d="m2 2 5 5"></path><path d="m9.5 9.5 5 5"></path></svg>'), pointer;
  }
</style>