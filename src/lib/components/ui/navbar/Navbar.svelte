<script lang="ts">
  import { fade, fly } from "svelte/transition";
  import { Menu, X, Leaf } from "@lucide/svelte";

  let { activeCategory = $bindable() } = $props();
  let menuOpen = $state(false);
  let isScrolled = $state(false);

  const navLinks = [
    { name: "Home", icon: "🏠", target: "home" },
    { name: "Library", icon: "📚", target: "archive" },
    // { name: "Showcase", icon: "📜", target: "showcase" },
    { name: "About", icon: "🦊", target: "about" },
  ];

  if (typeof window !== "undefined") {
    window.onscroll = () => {
      isScrolled = window.scrollY > 20;
    };
  }

  function selectMenu(name: string, target?: string) {
    activeCategory = name;
    menuOpen = false;

    if (!target) return;

    const el = document.getElementById(target);
    if (!el) return;

    el.scrollIntoView({
      behavior: "smooth",
      block: "start",
    });
  }
</script>

<nav class="fixed top-0 left-0 right-0 z-100 transition-all duration-500 {isScrolled ? 'py-2' : 'py-6 md:py-10'}">
  <div class="max-w-7xl mx-auto px-4 md:px-8">
    <div class="flex items-center justify-between">
      <button
        onclick={() => selectMenu("Home", "home")}
        class="group relative flex items-center bg-[#fdf6e3] border-[3px] border-[#283618] p-1 shadow-[4px_4px_0px_0px_#bc6c25] hover:shadow-none hover:translate-x-1 hover:translate-y-1 transition-all"
      >
        <div class="bg-[#606c38] p-2 border-2 border-[#283618]">
          <Leaf size={22} class="text-white group-hover:rotate-45 transition-transform" />
        </div>
        <div class="px-3 py-1 bg-[#fdf6e3]">
          <h1 class="font-['VT323'] text-2xl text-[#2d2d2d] leading-none uppercase tracking-tighter">Khwarizmi</h1>
          <p class="font-['VT323'] text-[10px] text-[#bc6c25] leading-none uppercase tracking-[0.2em]">Spirit of Pixel</p>
        </div>
      </button>

      <div class="hidden md:flex items-center gap-3">
        {#each navLinks as link}
          <button
            onclick={() => selectMenu(link.name, link.target)}
            class="group relative px-5 py-2 flex items-center gap-2 bg-[#fdf6e3] border-[3px] border-[#283618] transition-all
            {activeCategory === link.name ? 'bg-[#606c38] text-white -translate-y-1 shadow-[4px_4px_0px_0px_#283618]' : 'text-[#2d2d2d] hover:-translate-y-1 hover:shadow-[4px_4px_0px_0px_#bc6c25]'}"
          >
            <span class="text-sm group-hover:scale-125 transition-transform">{link.icon}</span>
            <span class="font-['VT323'] text-xl uppercase tracking-widest">{link.name}</span>

            {#if activeCategory === link.name}
              <div in:fade class="absolute -bottom-6 left-1/2 -translate-x-1/2 text-[#606c38] animate-bounce">▲</div>
            {/if}
          </button>
        {/each}
      </div>

      <button
        class="md:hidden size-12 bg-[#dda15e] border-[3px] border-[#283618] shadow-[4px_4px_0px_0px_#283618] flex items-center justify-center text-white active:shadow-none active:translate-y-1 transition-all"
        onclick={() => (menuOpen = !menuOpen)}
      >
        {#if menuOpen}
          <X size={28} />
        {:else}
          <Menu size={28} />
        {/if}
      </button>
    </div>
  </div>

  {#if menuOpen}
    <div transition:fade={{ duration: 300 }} class="fixed inset-0 bg-[#f1f0e8] z-[-1] flex flex-col items-center justify-center p-6 overflow-hidden">
      <div class="absolute inset-0 opacity-10 bg-[url('https://www.transparenttextures.com/patterns/p6.png')]"></div>

      <div class="absolute top-10 left-10 text-6xl animate-pulse">☁️</div>
      <div class="absolute bottom-20 right-10 text-6xl animate-bounce">🌿</div>

      <div class="flex flex-col gap-5 w-full max-w-xs relative z-10">
        {#each navLinks as link, i}
          <button
            in:fly={{ y: 20, delay: i * 100 }}
            onclick={() => selectMenu(link.name, link.target)}
            class="w-full bg-white border-4 border-[#283618] p-4 flex items-center justify-between shadow-[6px_6px_0px_0px_#bc6c25] active:shadow-none active:translate-x-1 active:translate-y-1 transition-all"
          >
            <span class="font-['VT323'] text-4xl text-[#2d2d2d] uppercase tracking-tighter">{link.name}</span>
            <span class="text-3xl">{link.icon}</span>
          </button>
        {/each}
      </div>
    </div>
  {/if}
</nav>

<style>
  nav {
    -webkit-font-smoothing: none;
    image-rendering: pixelated;
  }
</style>
