<script lang="ts">
    // Svelte 5 Props
    let { creator = "Khwarizmi" } = $props();
    const year = new Date().getFullYear();

    // Data Ikon Sosial Media (Pixel Style SVG Paths)
    const socialPlatforms = [
        { 
            name: "GitHub", 
            color: "hover:bg-[#24292e]", 
            icon: "M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.012 8.012 0 0 0 16 8c0-4.42-3.58-8-8-8z"
        },
        { 
            name: "Twitter", 
            color: "hover:bg-[#1DA1F2]", 
            icon: "M23.953 4.57a10 10 0 01-2.825.775 4.958 4.958 0 002.163-2.723c-.951.555-2.005.959-3.127 1.184a4.92 4.92 0 00-8.384 4.482C7.69 8.095 4.067 6.13 1.64 3.162a4.822 4.822 0 00-.666 2.475c0 1.71.87 3.213 2.188 4.096a4.904 4.904 0 01-2.228-.616v.06a4.923 4.923 0 003.946 4.827 4.996 4.996 0 01-2.212.085 4.936 4.936 0 004.604 3.417 9.867 9.867 0 01-6.102 2.105c-.39 0-.779-.023-1.17-.067a13.995 13.995 0 007.557 2.209c9.053 0 13.998-7.496 13.998-13.985 0-.21 0-.42-.015-.63A9.935 9.935 0 0024 4.59z"
        },
        { 
            name: "Email", 
            color: "hover:bg-[#EA4335]", 
            icon: "M20 4H4c-1.1 0-1.99.9-1.99 2L2 18c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"
        }
    ];
</script>

<svelte:head>
    <link href="https://fonts.googleapis.com/css2?family=VT323&display=swap" rel="stylesheet">
</svelte:head>

<footer class="relative mt-16 md:mt-32 w-full bg-white border-t-[4px] md:border-t-[8px] border-black overflow-hidden font-pixel group/footer">
    
    <div class="absolute inset-0 z-0 opacity-[0.03]" 
         style="background-image: linear-gradient(#000 1px, transparent 1px), linear-gradient(90deg, #000 1px, transparent 1px); background-size: 20px 20px;">
    </div>

    <div class="relative z-20 bg-[#0C7779] py-1 md:py-2 overflow-hidden flex whitespace-nowrap border-b-4 border-black shadow-[0_4px_0_rgba(0,0,0,0.1)]">
        <div class="animate-marquee flex gap-8 md:gap-12 items-center">
            {#each Array(8) as _}
                <span class="text-[#F3E5AB] font-bold text-sm md:text-xl uppercase tracking-[0.2em] md:tracking-[0.3em] flex items-center gap-4">
                    <span>•</span> PIXELATED REALITY <span>•</span> EST {year} <span>•</span> BEYOND THE SPIRIT WORLD 
                </span>
            {/each}
        </div>
    </div>

    <div class="relative z-10 max-w-7xl mx-auto px-4 md:px-6 pt-12 md:pt-20 pb-8 md:pb-12">
        <div class="flex flex-col items-center text-center gap-10 md:gap-14">
            
            <div class="cursor-default relative w-full flex flex-col items-center">
                <div class="hidden sm:block absolute -top-4 -left-2 md:-top-6 md:-left-10 w-6 h-6 md:w-8 md:h-8 border-4 border-[#0C7779] animate-spin-slow opacity-50"></div>
                <div class="hidden sm:block absolute -bottom-2 -right-2 md:-bottom-4 md:-right-10 w-4 h-4 md:w-6 md:h-6 bg-[#F3E5AB] border-2 border-black animate-bounce opacity-80"></div>

                <h2 class="relative text-[clamp(2.5rem,13vw,8rem)] font-black uppercase tracking-tighter leading-none transition-all duration-300">
                    <span class="absolute inset-0 text-transparent [-webkit-text-stroke:1px_black] md:[-webkit-text-stroke:2px_black] group-hover/footer:[-webkit-text-stroke:2px_#0C7779] transition-colors select-none" aria-hidden="true">
                        KHWARIZMI.GA
                    </span>
                    <span class="relative text-black group-hover:text-[#0C7779] transition-colors duration-300">
                        KHWARIZMI<span class="text-[#0C7779] group-hover:text-black">.</span>GA
                    </span>
                </h2>
                
                <div class="flex items-center justify-center gap-2 md:gap-4 mt-4 md:mt-6">
                    <div class="h-[2px] w-4 md:w-8 bg-black"></div>
                    <div class="h-[2px] w-1 md:w-2 bg-[#0C7779]"></div>
                    <p class="text-sm md:text-xl text-slate-500 uppercase tracking-widest italic">
                        Digital Craft by <span class="text-black font-black bg-[#F3E5AB] px-1 md:px-2">{creator}</span>
                    </p>
                    <div class="h-[2px] w-1 md:w-2 bg-[#0C7779]"></div>
                    <div class="h-[2px] w-4 md:w-8 bg-black"></div>
                </div>
            </div>

            <nav class="flex flex-wrap justify-center gap-3 md:gap-4 w-full" aria-label="Footer Navigation">
                {#each ['The Journey', 'Pixel Vault', 'Signal', 'Shrine'] as item}
                    <a 
                        href="#{item.toLowerCase().replace(' ', '')}" 
                        class="group/btn relative px-6 py-2 md:px-8 md:py-3 bg-white border-[3px] md:border-4 border-black text-lg md:text-2xl font-black uppercase transition-all
                               shadow-[4px_4px_0_0_#0C7779] md:shadow-[6px_6px_0_0_#0C7779] 
                               hover:shadow-[2px_2px_0_0_#000] hover:translate-x-1 hover:translate-y-1 
                               hover:bg-[#0C7779] hover:text-[#F3E5AB] overflow-hidden"
                    >
                        <span class="relative z-10">{item}</span>
                        <div class="absolute inset-0 bg-black translate-y-full group-hover/btn:translate-y-0 transition-transform duration-300 z-0"></div>
                    </a>
                {/each}
            </nav>
        </div>

        <div class="mt-12 md:mt-24 pt-6 md:pt-8 border-t-4 border-dashed border-slate-300 flex flex-col md:flex-row justify-between items-center gap-8 md:gap-8">
            
            <div class="flex items-center gap-3 md:gap-5">
                <div class="relative w-10 h-10 md:w-14 md:h-14 bg-white border-[3px] md:border-4 border-black flex items-center justify-center shadow-[3px_3px_0_0_#000] md:shadow-[4px_4px_0_0_#000] group">
                    <div class="absolute inset-0 bg-[#0C7779] opacity-0 group-hover:opacity-20 animate-ping"></div>
                    <div class="w-3 h-3 md:w-4 md:h-4 bg-[#0C7779] group-hover:bg-green-500 transition-colors"></div>
                    <div class="absolute -right-3 md:-right-4 top-1/2 h-1 w-3 md:w-4 bg-black"></div>
                </div>
                <div class="text-left pl-2 border-l-4 border-black">
                    <div class="text-[10px] md:text-xs text-slate-400 uppercase font-bold tracking-wider">System Status</div>
                    <div class="text-lg md:text-xl text-black font-black uppercase leading-none tracking-tight">
                        Online <span class="text-[#0C7779] animate-pulse">●</span>
                    </div>
                </div>
            </div>

            <div class="flex flex-col items-center md:items-end gap-4 w-full md:w-auto">
                <div class="flex gap-3 md:gap-4">
                    {#each socialPlatforms as platform}
                        <button 
                            type="button"
                            aria-label="Follow on {platform.name}"
                            title={platform.name}
                            class="group/social relative w-10 h-10 md:w-12 md:h-12 bg-white border-[3px] md:border-4 border-black shadow-[3px_3px_0_0_#0C7779] md:shadow-[4px_4px_0_0_#0C7779] {platform.color} hover:shadow-none hover:translate-x-1 hover:translate-y-1 transition-all flex items-center justify-center overflow-hidden"
                        >
                            <svg viewBox="0 0 24 24" fill="currentColor" class="w-5 h-5 md:w-6 md:h-6 text-black group-hover/social:text-white transition-colors z-10 relative">
                                <path d={platform.icon} />
                            </svg>
                            <div class="absolute inset-0 opacity-10 bg-[radial-gradient(circle,white_1px,transparent_1px)] [background-size:4px_4px] hidden group-hover/social:block"></div>
                        </button>
                    {/each}
                </div>
                <p class="text-[10px] md:text-xs text-slate-400 font-bold tracking-[0.2em] md:tracking-[0.3em] uppercase bg-slate-50 px-2 py-1 text-center md:text-right">
                    © {year} • Crafted in Bogor
                </p>
            </div>
        </div>
    </div>

    <div class="absolute bottom-0 left-0 w-full flex items-end opacity-10 pointer-events-none overflow-hidden">
        {#each Array(20) as _, i}
            <div class="w-4 md:w-8 bg-black mx-1" style="height: {Math.random() * 40 + 10}px"></div>
        {/each}
    </div>
</footer>

<style>
    .font-pixel {
        font-family: 'VT323', monospace;
    }

    @keyframes marquee {
        0% { transform: translateX(0); }
        100% { transform: translateX(-50%); }
    }
    
    @keyframes spin-slow {
        from { transform: rotate(0deg); }
        to { transform: rotate(360deg); }
    }

    .animate-marquee { animation: marquee 40s linear infinite; }
    .animate-spin-slow { animation: spin-slow 10s linear infinite; }

    footer {
        image-rendering: pixelated;
    }

    /* Utilitas untuk text outline/hollow - Responsive stroke width in class already */
    .-webkit-text-stroke {
        -webkit-text-stroke-color: black;
    }
</style>