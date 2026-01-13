<script lang="ts">
  import { onMount } from "svelte";
  import { register } from "swiper/element/bundle";
  import GameCard from "./GameCard.svelte";
  import { ChevronLeft, ChevronRight, Wind, Play, Sparkles, X, Ghost } from "@lucide/svelte";
  import { fade, fly, scale } from "svelte/transition";

  // Registrasi Swiper
  register();

  // Props
  let { filter = "All Games" } = $props();

  // Types
  type Game = {
    id: number;
    title: string;
    category: string;
    developer: string;
    img: string;
    description: string;
    link: string;
  };

  // State
  let selectedGame = $state<Game | null>(null);
  let swiperEl = $state<any>(null);

  // Data
  const allGames = [
    {
      id: 1,
      title: "Forest Spirit",
      category: "RPG",
      developer: "Khwarizmi",
      img: "https://images.unsplash.com/photo-1511497584788-d2be64177ee4?w=600&q=80",
      description: "Perjalanan spiritual di hutan terlarang untuk menemukan kembali jati diri yang hilang.",
      link: "#",
    },
    {
      id: 2,
      title: "Sky Journey",
      category: "Action",
      developer: "Khwarizmi",
      img: "https://images.unsplash.com/photo-1542601906-6617415170d3?w=600&q=80",
      description: "Terbang melintasi pulau terapung dengan sayap mekanik kuno.",
      link: "#",
    },
    {
      id: 3,
      title: "Summer Rain",
      category: "Experimental",
      developer: "Khwarizmi",
      img: "https://images.unsplash.com/photo-1515582239454-e74f1c9ddc37?w=600&q=80",
      description: "Simulasi melodi pixel lo-fi yang menenangkan di tengah hujan sore.",
      link: "#",
    },
    {
      id: 4,
      title: "Ancient Ruins",
      category: "RPG",
      developer: "Khwarizmi",
      img: "https://images.unsplash.com/photo-1616422891907-742880c98fce?w=600&q=80",
      description: "Eksplorasi reruntuhan kuno yang dipenuhi teka-teki logika matematika.",
      link: "#",
    },
    {
      id: 5,
      title: "Santri Bross",
      category: "RPG",
      developer: "Khwarizmi",
      img: "https://images.unsplash.com/photo-1616422891907-742880c98fce?w=600&q=80",
      description: "Eksplorasi reruntuhan kuno yang dipenuhi teka-teki logika matematika.",
      link: "#",
    },
    {
      id: 6,
      title: "Writting Hijaiyah",
      category: "RPG",
      developer: "Khwarizmi",
      img: "https://images.unsplash.com/photo-1616422891907-742880c98fce?w=600&q=80",
      description: "Eksplorasi reruntuhan kuno yang dipenuhi teka-teki logika matematika.",
      link: "#",
    },
  ];

  // Derived Logic
  let filteredGames = $derived(filter === "All Games" ? allGames : allGames.filter((g) => g.category === filter));

  // Swiper Init
  onMount(() => {
    const params = {
      slidesPerView: 1.15,
      spaceBetween: 24,
      centeredSlides: true,

      // --- PERUBAHAN DISINI ---
      loop: true, // Aktifkan infinite loop
      // rewind: true,   // Hapus atau comment ini (konflik dengan loop)
      // ------------------------

      breakpoints: {
        640: { slidesPerView: 1.5, spaceBetween: 20 },
        768: { slidesPerView: 2.2, spaceBetween: 24 },
        1024: { slidesPerView: 3, spaceBetween: 32 },
      },
      observer: true,
      observeParents: true,
    };

    Object.assign(swiperEl, params);
    swiperEl.initialize();
  });

  function closeModal() {
    selectedGame = null;
  }

  // Navigasi Swiper
  const handlePrev = () => swiperEl?.swiper?.slidePrev();
  const handleNext = () => swiperEl?.swiper?.slideNext();

  // Re-update swiper saat filter berubah
  $effect(() => {
    // Kita perlu dependensi ke filteredGames agar effect jalan saat filter berubah
    const games = filteredGames;

    if (swiperEl && swiperEl.swiper) {
      // Tunggu DOM render slide baru, lalu update
      setTimeout(() => {
        // Saat data berubah, loop mode perlu re-init agar indexnya benar
        swiperEl.swiper.loopDestroy();
        swiperEl.swiper.loopCreate();
        swiperEl.swiper.update();
        swiperEl.swiper.slideToLoop(0); // Reset ke awal loop
      }, 50);
    }
  });
</script>

{#if selectedGame}
  <div transition:fade={{ duration: 200 }} class="fixed inset-0 bg-[#2d2d2d]/90 backdrop-blur-sm z-[9999] flex items-center justify-center p-4">
    <button class="absolute inset-0 w-full h-full cursor-default" onclick={closeModal} aria-label="Close modal"></button>

    <div transition:scale={{ start: 0.95, duration: 300 }} class="relative w-full max-w-5xl bg-[#fdf6e3] border-[4px] border-[#2d2d2d] shadow-[16px_16px_0px_#2d2d2d] flex flex-col md:flex-row overflow-hidden">
      <div class="h-8 bg-[#2d2d2d] flex items-center px-4 justify-between md:hidden">
        <span class="text-white font-['VT323']">FILE: {selectedGame.id}_LOG</span>
        <button onclick={closeModal} class="text-white"><X size={18} /></button>
      </div>

      <button
        onclick={closeModal}
        class="hidden md:flex absolute top-4 right-4 z-20 size-12 bg-white border-2 border-[#2d2d2d] items-center justify-center shadow-[4px_4px_0px_#2d2d2d] hover:bg-[#bc6c25] hover:text-white hover:translate-x-1 hover:translate-y-1 hover:shadow-none transition-all"
      >
        <X size={24} />
      </button>

      <div class="relative w-full md:w-5/12 aspect-video md:aspect-auto border-b-4 md:border-b-0 md:border-r-4 border-[#2d2d2d] bg-[#2d2d2d] group overflow-hidden">
        <img src={selectedGame.img} alt={selectedGame.title} class="size-full object-cover opacity-90 transition-transform duration-1000 group-hover:scale-110" style="image-rendering: pixelated;" />
        <div
          class="absolute inset-0 bg-[linear-gradient(rgba(18,16,16,0)_50%,rgba(0,0,0,0.25)_50%),linear-gradient(90deg,rgba(255,0,0,0.06),rgba(0,255,0,0.02),rgba(0,0,255,0.06))] z-10 pointer-events-none bg-[length:100%_4px,6px_100%]"
        ></div>
        <div class="absolute inset-0 bg-gradient-to-t from-[#2d2d2d] via-transparent to-transparent opacity-60"></div>
        <div class="absolute bottom-4 left-4 z-20">
          <span class="bg-[#bc6c25] text-white px-2 py-1 font-['VT323'] text-lg border border-white/20">IMG_SEQ_0{selectedGame.id}</span>
        </div>
      </div>

      <div class="relative w-full md:w-7/12 p-8 md:p-12 flex flex-col bg-[#fdf6e3]">
        <div class="absolute inset-0 opacity-10 bg-[radial-gradient(#2d2d2d_1px,transparent_1px)] bg-[size:24px_24px] pointer-events-none"></div>

        <div class="relative z-10 flex flex-col h-full justify-between">
          <div>
            <div class="flex items-center gap-3 mb-2">
              <span class="font-['VT323'] text-[#606c38] tracking-widest uppercase text-base border border-[#606c38] px-2 py-0.5 bg-[#606c38]/10 rounded">
                System: {selectedGame.category}
              </span>
              <span class="h-px flex-1 bg-[#2d2d2d]/20"></span>
            </div>

            <h3 class="font-['VT323'] text-5xl md:text-6xl text-[#2d2d2d] leading-[0.9] uppercase mb-6 drop-shadow-sm">
              {selectedGame.title}
            </h3>

            <div class="relative pl-6 py-2 border-l-4 border-[#bc6c25]">
              <p class="font-['VT323'] text-2xl text-[#5d4037] leading-tight">
                "{selectedGame.description}"
              </p>
            </div>
          </div>

          <div class="mt-8 md:mt-0 pt-8 border-t-2 border-[#2d2d2d]/10 border-dashed">
            <a
              href={selectedGame.link}
              target="_blank"
              class="group relative block w-full bg-[#2d2d2d] text-[#fdf6e3] py-4 text-center font-['VT323'] text-3xl overflow-hidden shadow-[6px_6px_0px_#bc6c25] hover:shadow-[2px_2px_0px_#bc6c25] hover:translate-x-1 hover:translate-y-1 transition-all active:bg-[#bc6c25]"
            >
              <span class="relative z-10 flex items-center justify-center gap-3">
                <Play size={24} class="fill-current" /> INITIALIZE_GAME
              </span>
              <div class="absolute inset-0 bg-white/10 translate-y-full group-hover:translate-y-0 transition-transform duration-300"></div>
            </a>

            <div class="flex justify-between mt-3 text-[#5d4037]/60 font-['VT323'] text-sm uppercase">
              <span>Dev: {selectedGame.developer}</span>
              <span class="animate-pulse">Status: Online</span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
{/if}

<div class="relative group px-4 md:px-0 max-w-7xl mx-auto">
  <div class="flex flex-col md:flex-row justify-between items-end mb-10 gap-6">
    <div class="flex items-center gap-3 text-[#606c38] font-['VT323'] text-2xl italic opacity-80 bg-[#fdf6e3] px-4 py-2 border border-[#606c38]/20 rounded-lg shadow-sm">
      <Wind size={20} class="animate-pulse" />
      <span>Searching Realm: <span class="text-[#bc6c25] font-bold uppercase">{filter}</span></span>
    </div>

    <div class="flex gap-4">
      <button
        onclick={handlePrev}
        class="size-14 bg-[#fdf6e3] text-[#2d2d2d] border-2 border-[#2d2d2d] flex items-center justify-center shadow-[4px_4px_0px_#2d2d2d] hover:-rotate-2 hover:bg-white hover:shadow-[6px_6px_0px_#bc6c25] active:translate-x-1 active:translate-y-1 active:shadow-none transition-all duration-300 rounded-lg"
        aria-label="Previous Slide"
      >
        <ChevronLeft size={32} />
      </button>
      <button
        onclick={handleNext}
        class="size-14 bg-[#2d2d2d] text-[#fdf6e3] border-2 border-[#2d2d2d] flex items-center justify-center shadow-[4px_4px_0px_#bc6c25] hover:rotate-2 hover:bg-[#606c38] hover:border-[#606c38] active:translate-x-1 active:translate-y-1 active:shadow-none transition-all duration-300 rounded-lg"
        aria-label="Next Slide"
      >
        <ChevronRight size={32} />
      </button>
    </div>
  </div>

  <div class="min-h-[400px]">
    {#if filteredGames.length > 0}
      <swiper-container bind:this={swiperEl} init="false" class="py-8 px-2" loop="true">
        {#each filteredGames as game (game.id)}
          <swiper-slide class="pb-12 pt-4 px-2">
            <GameCard {game} onOpenPreview={(g: Game) => (selectedGame = g)} />
          </swiper-slide>
        {/each}
      </swiper-container>
    {:else}
      <div in:fade class="flex flex-col items-center justify-center py-20 text-center border-4 border-dashed border-[#2d2d2d]/10 rounded-3xl bg-[#fdf6e3]/30">
        <div class="mb-4 text-[#bc6c25] opacity-50">
          <Ghost size={64} strokeWidth={1.5} />
        </div>
        <h3 class="font-['VT323'] text-4xl text-[#2d2d2d] mb-2">No Signals Detected</h3>
        <p class="font-['VT323'] text-xl text-[#5d4037] max-w-md">
          Sector <span class="text-[#bc6c25] font-bold">"{filter}"</span> appears to be empty. <br /> Try exploring another coordinate?
        </p>
      </div>
    {/if}
  </div>
</div>
