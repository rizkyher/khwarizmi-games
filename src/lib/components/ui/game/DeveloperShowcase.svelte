<script lang="ts">
  import { onMount } from "svelte";
  import { Sparkles, ChevronLeft, ChevronRight } from "@lucide/svelte";
  import { register } from "swiper/element/bundle";

  // Register Swiper Web Component
  register();

  const team = [
    { name: "Bayyu", role: "Logic Architect", avatar: "🌿", bio: "Master of algorithms and spirit mechanics.", color: "#a7c957" },
    { name: "Farhan", role: "Visual Weaver", avatar: "🎨", bio: "Painting pixels with watercolor dreams.", color: "#f1f0e8" },
    { name: "Zaidan", role: "World Builder", avatar: "🪵", bio: "Crafting the foundations of our digital forest.", color: "#bc6c25" },
    { name: "Farhan", role: "Sound Alchemist", avatar: "🎐", bio: "Capturing the whispers of the wind.", color: "#a8dadc" },
    { name: "Farrel", role: "Interface Guide", avatar: "📜", bio: "Designing paths for lost souls to follow.", color: "#606c38" },
    { name: "Arif", role: "System Guardian", avatar: "🛡️", bio: "Ensuring the realm stays stable and safe.", color: "#283618" },
    { name: "Zain", role: "Writing Hijaiyyah", avatar: "✍️", bio: "Preserving sacred scripts in the digital age.", color: "#dda15e" },
  ];

  let swiperEl: any;

  onMount(() => {
    // 1. Definisikan Parameter di sini (Bukan di HTML)
    const swiperParams = {
      slidesPerView: 1,
      spaceBetween: 30,
      loop: true,
      speed: 800, // Menambah kehalusan animasi
      breakpoints: {
        640: { slidesPerView: 2 },
        1024: { slidesPerView: 3 },
      },
    };

    // 2. Inject parameter ke elemen Swiper
    Object.assign(swiperEl, swiperParams);

    // 3. Inisialisasi manual
    swiperEl.initialize();
  });

  // 4. Safe Navigation (Menggunakan Optional Chaining ?.)
  const goNext = () => {
    swiperEl?.swiper?.slideNext();
  };

  const goPrev = () => {
    swiperEl?.swiper?.slidePrev();
  };
</script>

<section id="about" class="relative py-32 bg-[#fdf6e3] overflow-hidden border-y-4 border-[#2d2d2d]">
  <div
    class="absolute inset-0 opacity-[0.03] pointer-events-none
    bg-[radial-gradient(#2d2d2d_2px,transparent_2px)]
    bg-size-[32px_32px]"
  ></div>

  <div class="max-w-6xl mx-auto px-6 relative z-10">
    <div class="flex flex-col md:flex-row items-end justify-between mb-16 gap-6">
      <div class="space-y-4">
        <div
          class="inline-flex items-center gap-3 px-4 py-1.5
          bg-[#606c38] text-[#fefae0] border-2 border-[#2d2d2d]
          shadow-[4px_4px_0px_#2d2d2d]"
        >
          <Sparkles size={16} />
          <span class="font-['VT323'] text-lg uppercase tracking-[0.2em]"> Personnel_Archive </span>
        </div>

        <h2 class="font-['VT323'] text-6xl text-[#2d2d2d] uppercase tracking-tighter">
          The <span class="italic text-[#bc6c25]">Storytellers</span>
        </h2>
      </div>

      <div class="flex gap-4">
        <button
          onclick={goPrev}
          class="size-14 bg-white border-3 border-[#2d2d2d]
          flex items-center justify-center shadow-[4px_4px_0px_#2d2d2d]
          active:translate-x-1 active:translate-y-1 active:shadow-none transition-all"
        >
          <ChevronLeft />
        </button>

        <button
          onclick={goNext}
          class="size-14 bg-[#bc6c25] border-3 border-[#2d2d2d]
          flex items-center justify-center shadow-[4px_4px_0px_#2d2d2d]
          active:translate-x-1 active:translate-y-1 active:shadow-none transition-all"
        >
          <ChevronRight class="text-white" />
        </button>
      </div>
    </div>

    <swiper-container bind:this={swiperEl} init="false" class="w-full">
      {#each team as member}
        <swiper-slide class="p-4 h-auto flex">
          <div class="group relative w-full perspective-1000">
            <div
              class="absolute inset-0 bg-[#2d2d2d] rounded-sm translate-x-2 translate-y-2
                group-hover:translate-x-4 group-hover:translate-y-4 transition-all duration-300"
            ></div>

            <div
              class="relative h-full bg-[#fdf6e3] border-4 border-[#2d2d2d] p-8
             flex flex-col items-center text-center overflow-hidden
             group-hover:-translate-x-1 group-hover:-translate-y-1 transition-all duration-300"
            >
              <div
                class="absolute -top-10 -right-10 size-32 rounded-full blur-3xl opacity-0
                  group-hover:opacity-40 transition-opacity duration-500 pointer-events-none"
                style="background-color: {member.color};"
              ></div>

              <div class="relative size-24 mb-6 flex items-center justify-center">
                <div
                  class="absolute inset-0 border-2 border-dashed border-[#606c38]/40 rounded-full
                    animate-[spin_10s_linear_infinite] group-hover:border-[#bc6c25]"
                ></div>

                <div
                  class="text-6xl z-10 filter drop-shadow-[4px_4px_0px_rgba(0,0,0,0.1)]
                    group-hover:scale-125 group-hover:rotate-12 transition-transform duration-300 select-none"
                >
                  {member.avatar}
                </div>

                <div class="absolute -top-2 -right-2 opacity-0 group-hover:opacity-100 group-hover:animate-pulse transition-opacity text-xl">✨</div>
              </div>

              <div class="space-y-1 z-10">
                <h4 class="font-['VT323'] text-4xl text-[#2d2d2d] tracking-tighter uppercase">
                  {member.name}
                </h4>

                <div
                  class="inline-block px-3 py-0.5 bg-[#606c38] text-[#fefae0] text-sm font-['VT323']
                    uppercase tracking-widest transform -rotate-1 group-hover:rotate-1 transition-transform"
                >
                  {member.role}
                </div>
              </div>

              <div class="relative mt-6 pt-6 border-t-2 border-dotted border-[#2d2d2d]/20 w-full grow flex items-center justify-center">
                <div class="absolute -top-3 left-1/2 -translate-x-1/2 bg-[#fdf6e3] px-2">
                  <span class="text-[#bc6c25] text-xs opacity-50 uppercase font-bold tracking-tighter">Bio_Log</span>
                </div>

                <p class="font-['VT323'] text-xl text-[#5d4037] italic leading-tight group-hover:text-[#2d2d2d] transition-colors">
                  "{member.bio}"
                </p>
              </div>

              <div class="absolute bottom-2 right-2 opacity-0 group-hover:opacity-30 group-hover:-translate-y-2 transition-all duration-700 text-2xl">🦋</div>
            </div>
          </div>
        </swiper-slide>
      {/each}
    </swiper-container>
  </div>
</section>

<style>
  /* Fix layout issues with swiper web component */
  swiper-container {
    display: block;
    width: 100%;
  }

  .perspective-1000 {
    perspective: 1000px;
  }
</style>
