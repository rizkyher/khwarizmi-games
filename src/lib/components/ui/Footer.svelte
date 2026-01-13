<script lang="ts">
    // Svelte 5 Props
    let { creator = "Khwarizmi" } = $props();
    const year = new Date().getFullYear();

    const socialPlatforms = [
        { name: "GitHub", icon: "M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.012 8.012 0 0 0 16 8c0-4.42-3.58-8-8-8z" },
        { name: "Twitter", icon: "M23.953 4.57a10 10 0 01-2.825.775 4.958 4.958 0 002.163-2.723c-.951.555-2.005.959-3.127 1.184a4.92 4.92 0 00-8.384 4.482C7.69 8.095 4.067 6.13 1.64 3.162a4.822 4.822 0 00-.666 2.475c0 1.71.87 3.213 2.188 4.096a4.904 4.904 0 01-2.228-.616v.06a4.923 4.923 0 003.946 4.827 4.996 4.996 0 01-2.212.085 4.936 4.936 0 004.604 3.417 9.867 9.867 0 01-6.102 2.105c-.39 0-.779-.023-1.17-.067a13.995 13.995 0 007.557 2.209c9.053 0 13.998-7.496 13.998-13.985 0-.21 0-.42-.015-.63A9.935 9.935 0 0024 4.59z" },
        { name: "Email", icon: "M20 4H4c-1.1 0-1.99.9-1.99 2L2 18c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z" }
    ];
</script>

<svelte:head>
    <link href="https://fonts.googleapis.com/css2?family=Press+Start+2P&family=VT323&display=swap" rel="stylesheet">
</svelte:head>

<footer class="relative mt-20 w-full bg-[#1A2E29] border-t-8 border-[#41B78E] overflow-hidden text-[#E0F2F1] group/footer pb-10">
    
    <div class="absolute inset-0 opacity-10 pointer-events-none" 
         style="background-image: linear-gradient(#41B78E 2px, transparent 2px), linear-gradient(90deg, #41B78E 2px, transparent 2px); background-size: 40px 40px;">
    </div>

    <div class="bg-[#41B78E] py-2 border-b-4 border-black/30 shadow-lg overflow-hidden relative z-10">
        <div class="animate-marquee whitespace-nowrap flex gap-16 items-center">
            {#each Array(10) as _}
                <span class="text-white font-['VT323'] text-xl uppercase tracking-[0.2em] font-bold">
                    Start Your Adventure <span class="text-[#F9BA72] mx-2 text-2xl">•</span> Crafted with Pixels <span class="text-[#F9BA72] mx-2 text-2xl">•</span>
                </span>
            {/each}
        </div>
    </div>

    <div class="relative z-10 max-w-7xl mx-auto px-6 pt-16 flex flex-col items-center text-center">
        
        <div class="mb-10 relative group cursor-default">
            
            <div class="absolute -left-16 top-1/2 -translate-x-1/2 w-12 h-8 bg-white/10 hidden md:block animate-pulse"></div>
            <div class="absolute -right-16 top-1/2 -translate-x-1/2 w-12 h-8 bg-white/10 hidden md:block animate-pulse" style="animation-delay: 1s"></div>

            <h1 class="text-4xl md:text-6xl lg:text-7xl uppercase leading-tight transform transition-transform duration-300 hover:scale-105"
                style="
                    font-family: 'Press Start 2P', cursive; 
                    color: white;
                    text-shadow: 
                        4px 4px 0px #41B78E, 
                        8px 8px 0px #000;
                ">
                KHWARIZMI<span class="text-[#F9BA72]">.GA</span>
            </h1>
            
            <div class="mt-6 inline-block bg-black border-2 border-[#41B78E] px-4 py-1 shadow-[4px_4px_0_0_#41B78E]">
                <p class="font-['VT323'] text-xl md:text-2xl text-[#F9BA72] tracking-[0.3em] uppercase">
                    The Digital Studio
                </p>
            </div>
        </div>

        <nav class="flex flex-wrap justify-center gap-4 md:gap-6 mb-12">
            {#each ['Games', 'About', 'Team', 'Contact'] as item}
                <a href="#{item.toLowerCase()}" 
                   class="relative px-6 py-3 bg-[#41B78E] border-4 border-[#2A7A5E] text-white font-['VT323'] text-xl md:text-2xl uppercase tracking-widest transition-all
                          hover:-translate-y-1 hover:bg-[#F9BA72] hover:text-black hover:border-black hover:shadow-[0_6px_0_0_black] shadow-[0_4px_0_0_#1A2E29]">
                    {item}
                </a>
            {/each}
        </nav>

        <div class="w-full border-t-4 border-[#41B78E] pt-8 flex flex-col md:flex-row justify-between items-center gap-6">
            
            <div class="flex items-center gap-3">
                <div class="w-3 h-3 bg-[#41B78E] animate-ping"></div>
                <p class="font-['VT323'] text-xl text-[#A7F3D0]">
                    © {year} {creator}. All rights reserved.
                </p>
            </div>

            <div class="flex gap-4">
                {#each socialPlatforms as platform}
                    <button 
                        class="w-10 h-10 bg-white border-2 border-black flex items-center justify-center shadow-[3px_3px_0_0_#41B78E] transition-transform active:translate-y-1 active:shadow-none hover:bg-[#F9BA72] group/icon"
                        aria-label={platform.name}
                        title={platform.name}
                    >
                        <svg viewBox="0 0 24 24" fill="currentColor" class="w-5 h-5 text-black" aria-hidden="true">
                            <path d={platform.icon} />
                        </svg>
                    </button>
                {/each}
            </div>
        </div>

    </div>
</footer>

<style>
    @keyframes marquee {
        0% { transform: translateX(0); }
        100% { transform: translateX(-50%); }
    }
    .animate-marquee { animation: marquee 30s linear infinite; }
</style>