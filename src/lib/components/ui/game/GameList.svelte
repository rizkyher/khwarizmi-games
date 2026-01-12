<script lang="ts">
  import { onMount } from "svelte";
  import { register } from "swiper/element/bundle";
  import GameCard from "./GameCard.svelte";
  import { ChevronLeft, ChevronRight, Wind, Play, Sparkles } from "@lucide/svelte";
  import { fade, scale } from "svelte/transition";

  // Registrasi Swiper
  register();

  // Props Svelte 5
  let { filter = "All Games" } = $props();

  // Definisi Tipe Data
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
  let swiperEl = $state<any>(null); // Referensi ke elemen Swiper

  // Data
  const allGames = [
    { id: 1, title: "Forest Spirit", category: "RPG", developer: "Khwarizmi", img: "https://images.unsplash.com/photo-1511497584788-d2be64177ee4?w=600&q=80", description: "Perjalanan spiritual di hutan terlarang.", link: "#" },
    { id: 2, title: "Sky Journey", category: "Action", developer: "Khwarizmi", img: "https://images.unsplash.com/photo-1542601906-6617415170d3?w=600&q=80", description: "Terbang melintasi pulau terapung.", link: "#" },
    { id: 3, title: "Summer Rain", category: "Experimental", developer: "Khwarizmi", img: "https://images.unsplash.com/photo-1515582239454-e74f1c9ddc37?w=600&q=80", description: "Melodi pixel di tengah hujan.", link: "#" },
    { id: 4, title: "Ancient Ruins", category: "RPG", developer: "Khwarizmi", img: "https://images.unsplash.com/photo-1616422891907-742880c98fce?w=600&q=80", description: "Eksplorasi reruntuhan kuno.", link: "#" },
  ];

  // Derived State (Filter Logic)
  let filteredGames = $derived(filter === "All Games" ? allGames : allGames.filter((g) => g.category === filter));

  // Inisialisasi Swiper
  onMount(() => {
    const params = {
      slidesPerView: 1.15,
      spaceBetween: 16,
      centeredSlides: true,
      loop: true,
      breakpoints: {
        768: { slidesPerView: 2.2 },
        1024: { slidesPerView: 3 },
      },
      // Opsional: Observer agar swiper update saat elemen dom berubah
      observer: true,
      observeParents: true,
    };

    // Inject params & initialize
    Object.assign(swiperEl, params);
    swiperEl.initialize();
  });

  // Helper Functions
  function closeModal() {
    selectedGame = null;
  }

  // Navigasi Aman (Menggunakan Optional Chaining ?.)
  const handlePrev = () => swiperEl?.swiper?.slidePrev();
  const handleNext = () => swiperEl?.swiper?.slideNext();

  // Effect: Jika filter berubah, minta swiper update (opsional tapi disarankan)
  $effect(() => {
    if (swiperEl && swiperEl.swiper) {
      // Tunggu DOM render slide baru, lalu update swiper
      setTimeout(() => {
        swiperEl.swiper.update();
      }, 50);
    }
    // Dependency tracking otomatis via $derived filteredGames
    filteredGames;
  });
</script>

{#if selectedGame}
  <div transition:fade={{ duration: 200 }} class="fixed inset-0 bg-[#2d2d2d]/80 backdrop-blur-sm z-9999 flex items-center justify-center p-4">
    <button class="absolute inset-0 w-full h-full cursor-default" onclick={closeModal} aria-label="Close modal"></button>

    <div transition:scale={{ start: 0.9, duration: 300 }} class="relative bg-[#fdf6e3] border-4 border-[#2d2d2d] shadow-[12px_12px_0px_#2d2d2d] overflow-hidden max-w-4xl w-full flex flex-col md:flex-row">
      <button onclick={closeModal} class="absolute top-4 right-4 z-10 size-10 bg-white border-2 border-[#2d2d2d] flex items-center justify-center shadow-[3px_3px_0px_#2d2d2d] hover:bg-[#bc6c25] hover:text-white transition-all">✕</button>

      <div class="w-full md:w-1/2 aspect-video md:aspect-auto bg-[#d9e4dd] border-b-4 md:border-b-0 md:border-r-4 border-[#2d2d2d]">
        <img src={selectedGame.img} alt={selectedGame.title} class="size-full object-cover" style="image-rendering: pixelated;" />
      </div>

      <div class="w-full md:w-1/2 p-8 flex flex-col justify-center bg-[radial-gradient(#2d2d2d_1px,transparent_1px)] bg-size-[20px_20px]">
        <div class="mb-6">
          <span class="font-['VT323'] text-[#606c38] tracking-widest uppercase text-sm flex items-center gap-2"><Sparkles size={14} /> MISSION_LOG</span>
          <h3 class="font-['VT323'] text-5xl text-[#2d2d2d] leading-none uppercase mt-2">{selectedGame.title}</h3>
        </div>
        <p class="font-['VT323'] text-xl text-[#5d4037] leading-tight mb-8">"{selectedGame.description}"</p>
        <a
          href={selectedGame.link}
          target="_blank"
          class="bg-[#2d2d2d] text-white py-4 border-2 border-[#2d2d2d] font-['VT323'] text-2xl flex items-center justify-center gap-3 shadow-[4px_4px_0px_#bc6c25] hover:bg-[#606c38] transition-all"
        >
          <Play size={20} fill="currentColor" /> ENTER_REALM
        </a>
      </div>
    </div>
  </div>
{/if}

<div class="relative group px-4 md:px-0">
  <div class="flex justify-between items-end mb-8">
    <div class="flex items-center gap-2 text-[#606c38] font-['VT323'] text-2xl italic opacity-70">
      <Wind size={24} /> <span>Explore the pixel realms</span>
    </div>

    <div class="flex gap-4">
      <button onclick={handlePrev} class="size-14 bg-white border-3 border-[#2d2d2d] flex items-center justify-center shadow-[5px_5px_0px_#2d2d2d] active:shadow-none active:translate-x-1 active:translate-y-1 transition-all">
        <ChevronLeft size={32} />
      </button>
      <button onclick={handleNext} class="size-14 bg-[#606c38] text-white border-3 border-[#2d2d2d] flex items-center justify-center shadow-[5px_5px_0px_#2d2d2d] active:shadow-none active:translate-x-1 active:translate-y-1 transition-all">
        <ChevronRight size={32} />
      </button>
    </div>
  </div>

  <swiper-container bind:this={swiperEl} init="false" class="py-8">
    {#each filteredGames as game (game.id)}
      <swiper-slide class="pb-6">
        <GameCard {game} onOpenPreview={(g: Game) => (selectedGame = g)} />
      </swiper-slide>
    {/each}
  </swiper-container>
</div>
