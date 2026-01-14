<script lang="ts">
    import { fade, scale } from 'svelte/transition';
    import { onMount, onDestroy } from 'svelte';

    export let game: {
        id: number;
        title: string;
        image: string;
        video?: string;
        desc: string;
        tags: string[];
<<<<<<< HEAD
    };

    let open = false;

    function close() {
        open = false;
=======
        image: string; // Updated from 'color' to 'image'
        video?: string;
>>>>>>> b937b935f088afba0ace05b8ff322769df3bb959
    }

    function onKey(e: KeyboardEvent) {
        if (e.key === 'Escape') close();
        if (e.key === 'Enter') open = true;
    }

    onMount(() => window.addEventListener('keydown', onKey));
    onDestroy(() => window.removeEventListener('keydown', onKey));
</script>

<!-- ================= CARD ================= -->
<div
    role="button"
    tabindex="0"
    on:click={() => (open = true)}
    class="relative w-[220px] md:w-[260px] h-[320px] md:h-[360px]
           bg-[#f8fafc] border-[4px] border-black
           rounded-xl overflow-hidden cursor-pointer
           shadow-[6px_6px_0_0_#000]"
>
    <!-- IMAGE -->
    <div class="relative h-[55%] border-b-[4px] border-black overflow-hidden">
        <img
            src={game.image}
            alt={game.title}
            class="w-full h-full object-cover"
        />

        <!-- CRT overlay -->
        <div
            class="pointer-events-none absolute inset-0
                   bg-[linear-gradient(rgba(18,16,16,0)_50%,rgba(0,0,0,0.15)_50%)]
                   bg-[length:100%_4px]"
        ></div>

<<<<<<< HEAD
        <!-- TAG -->
        <div class="absolute top-2 left-2 flex flex-wrap gap-1">
            {#each game.tags.slice(0, 2) as tag}
                <span
                    class="text-[8px] font-black uppercase tracking-widest
                           bg-yellow-400 px-1.5 py-0.5
                           border-2 border-black
                           shadow-[2px_2px_0_0_#000]"
                    style="font-family: 'Silkscreen', cursive;"
                >
                    {tag}
                </span>
            {/each}
=======
<div class="snap-center shrink-0 w-[260px] sm:w-[300px] md:w-[350px] py-4 font-pixel">
    <button 
        onmouseenter={() => isHovered = true}
        onmouseleave={() => isHovered = false}
        onclick={toggleModal}
        class="group relative w-full text-left bg-white border-[3px] md:border-4 border-black p-2 transition-all duration-300 
               {isHovered ? '-translate-y-2 md:-translate-y-4 shadow-[8px_8px_0_0_#0C7779] md:shadow-[12px_12px_0_0_#0C7779]' : 'shadow-[6px_6px_0_0_#000] md:shadow-[8px_8px_0_0_#000]'} 
               cursor-pointer outline-none block"
    >
        <div class="aspect-video border-4 border-black relative overflow-hidden bg-slate-900 group-hover:border-[#0C7779] transition-colors">
            
            <img 
                src={game.image} 
                alt={game.title} 
                class="absolute inset-0 w-full h-full object-cover transition-transform duration-500 ease-out {isHovered ? 'scale-110 blur-[1px]' : 'scale-100'}"
                loading="lazy"
            />
        <div class="aspect-video border-4 border-black relative overflow-hidden bg-slate-900 group-hover:border-[#0C7779] transition-colors">
            
            <img 
                src={game.image} 
                alt={game.title} 
                class="absolute inset-0 w-full h-full object-cover transition-transform duration-500 ease-out {isHovered ? 'scale-110 blur-[1px]' : 'scale-100'}"
                loading="lazy"
            />

            <div class="absolute inset-0 opacity-20 bg-[radial-gradient(#000_2px,transparent_1px)] [background-size:6px_6px] pointer-events-none"></div>
            <div class="absolute inset-0 opacity-20 bg-[radial-gradient(#000_2px,transparent_1px)] [background-size:6px_6px] pointer-events-none"></div>

            <span class="absolute top-2 left-2 z-10 text-white font-black text-2xl md:text-3xl drop-shadow-[2px_2px_0_#000]">
                #{game.id}
            </span>
            <span class="absolute top-2 left-2 z-10 text-white font-black text-2xl md:text-3xl drop-shadow-[2px_2px_0_#000]">
                #{game.id}
            </span>

            {#if isHovered}
                <div class="absolute inset-0 bg-[#0C7779]/60 flex items-center justify-center animate-fade">
                    <span class="bg-white text-black border-2 border-black px-4 py-1 font-bold text-lg shadow-[4px_4px_0_0_#000] -rotate-2">
                        VIEW DETAIL
                    </span>
                </div>
            {/if}
        </div>
            {#if isHovered}
                <div class="absolute inset-0 bg-[#0C7779]/60 flex items-center justify-center animate-fade">
                    <span class="bg-white text-black border-2 border-black px-4 py-1 font-bold text-lg shadow-[4px_4px_0_0_#000] -rotate-2">
                        VIEW DETAIL
                    </span>
                </div>
            {/if}
        </div>


        <div class="p-3 md:p-4 bg-white transition-colors">
            <h2 class="text-xl md:text-2xl font-black text-slate-900 uppercase mb-2 group-hover:text-[#0C7779] transition-colors leading-none truncate">
                {game.title}
            </h2>
            <div class="flex gap-2 flex-wrap">
                {#each game.tags.slice(0, 3) as tag} 
                    <span class="bg-white border-2 border-[#0C7779] px-1.5 py-0.5 text-xs md:text-sm font-bold uppercase shadow-[2px_2px_0_0_#0C7779]">
                {#each game.tags.slice(0, 3) as tag} 
                    <span class="bg-white border-2 border-[#0C7779] px-1.5 py-0.5 text-xs md:text-sm font-bold uppercase shadow-[2px_2px_0_0_#0C7779]">
                        {tag}
                    </span>
                {/each}
            </div>
        </div>
    </button>
</div>

{#if isModalOpen}
    <div 
        class="fixed inset-0 bg-[#0C7779]/90 backdrop-blur-sm z-[100] flex items-center justify-center p-4 md:p-6 overflow-hidden"
        onclick={toggleModal}
        onkeydown={(e) => e.key === 'Enter' && toggleModal()}
        role="presentation"
    >
        <div 
            role="dialog"
            aria-modal="true"
            tabindex="-1"
            class="bg-white border-[4px] md:border-8 border-black w-[95%] md:w-full max-w-3xl max-h-[90vh] md:max-h-none flex flex-col shadow-[10px_10px_0_0_#000] md:shadow-[20px_20px_0_0_#000] animate-modal-in outline-none font-pixel relative"
            onclick={(e) => e.stopPropagation()}
            onkeydown={(e) => e.stopPropagation()}
        >
            <div class="bg-[#0C7779] p-3 md:p-4 flex justify-between items-center text-white border-b-4 border-black shrink-0">
                <h2 class="text-2xl md:text-3xl font-black uppercase tracking-tighter truncate pr-4">Game Detail</h2>
                <button 
                    onclick={toggleModal} 
                    class="w-8 h-8 md:w-10 md:h-10 flex items-center justify-center bg-black text-white text-2xl md:text-3xl hover:bg-red-500 transition-colors border-2 border-white shadow-[2px_2px_0_0_rgba(0,0,0,0.5)] active:translate-y-1 active:shadow-none"
                    class="w-8 h-8 md:w-10 md:h-10 flex items-center justify-center bg-black text-white text-2xl md:text-3xl hover:bg-red-500 transition-colors border-2 border-white shadow-[2px_2px_0_0_rgba(0,0,0,0.5)] active:translate-y-1 active:shadow-none"
                    aria-label="Close modal"
                >
                    ×
                </button>
            </div>

            <div class="p-4 md:p-8 overflow-y-auto overscroll-contain">
                <div class="flex flex-col md:flex-row gap-6 md:gap-8">
                    
                    <div class="w-full md:w-1/2 shrink-0">
                        <div class="aspect-video md:aspect-square bg-slate-900 border-4 border-black flex items-center justify-center relative shadow-[6px_6px_0_0_#0C7779] mb-4 md:mb-0 overflow-hidden">
                            
                            <img 
                                src={game.image} 
                                alt={game.title} 
                                class="absolute inset-0 w-full h-full object-cover"
                            />

                            <div class="absolute inset-0 opacity-20 bg-[radial-gradient(#000_2px,transparent_1px)] [background-size:8px_8px] pointer-events-none"></div>
                        <div class="aspect-video md:aspect-square bg-slate-900 border-4 border-black flex items-center justify-center relative shadow-[6px_6px_0_0_#0C7779] mb-4 md:mb-0 overflow-hidden">
                            
                            <img 
                                src={game.image} 
                                alt={game.title} 
                                class="absolute inset-0 w-full h-full object-cover"
                            />

                            <div class="absolute inset-0 opacity-20 bg-[radial-gradient(#000_2px,transparent_1px)] [background-size:8px_8px] pointer-events-none"></div>
                        </div>
                    </div>

                    <div class="w-full md:w-1/2 space-y-4 md:space-y-6 flex flex-col">
                        <div>
                            <h3 class="text-3xl md:text-5xl font-black uppercase text-slate-800 underline decoration-[#0C7779] decoration-4 md:decoration-8 underline-offset-4 leading-none mb-3">
                                {game.title}
                            </h3>
                            
                            <div class="flex flex-wrap gap-2 mb-4">
                                {#each game.tags as tag}
                                    <span class="bg-[#0C7779] text-white text-xs md:text-sm px-2 py-1 font-bold uppercase border-2 border-black shadow-[2px_2px_0_0_#000]">{tag}</span>
                                {/each}
                            </div>
                        </div>

                        <p class="text-lg md:text-xl text-slate-600 leading-snug border-l-4 border-[#0C7779] pl-4 py-1 flex-grow">
                            {game.desc}
                        </p>

                        <button 
                            class="w-full py-3 md:py-4 bg-[#0C7779] text-white text-xl md:text-2xl font-black uppercase border-4 border-black shadow-[4px_4px_0_0_#000] md:shadow-[6px_6px_0_0_#000] hover:translate-x-1 hover:translate-y-1 hover:shadow-none active:scale-95 transition-all outline-none mt-auto hover:bg-[#0a6668]"
                            class="w-full py-3 md:py-4 bg-[#0C7779] text-white text-xl md:text-2xl font-black uppercase border-4 border-black shadow-[4px_4px_0_0_#000] md:shadow-[6px_6px_0_0_#000] hover:translate-x-1 hover:translate-y-1 hover:shadow-none active:scale-95 transition-all outline-none mt-auto hover:bg-[#0a6668]"
                        >
                            PLAY NOW →
                        </button>
                    </div>

                </div>
            </div>
>>>>>>> b937b935f088afba0ace05b8ff322769df3bb959
        </div>
    </div>

    <!-- CONTENT -->
    <div class="p-3 flex flex-col gap-2">
        <h3
            class="text-sm font-black uppercase leading-tight"
            style="font-family: 'Silkscreen', cursive;"
        >
            {game.title}
        </h3>

        <p class="text-[10px] text-slate-600 line-clamp-3">
            {game.desc}
        </p>
    </div>

    <!-- STATIC INDICATOR -->
    <div class="absolute bottom-2 right-2 flex items-center gap-1">
        <div class="w-2 h-2 bg-emerald-500 rounded-full animate-pulse"></div>
        <span
            class="text-[8px] font-bold tracking-widest text-slate-700"
            style="font-family: 'Silkscreen', cursive;"
        >
            DETAILS
        </span>
    </div>
</div>

<!-- ================= MODAL ================= -->
{#if open}
<div
    class="fixed inset-0 z-[9999] flex items-center justify-center"
    transition:fade
    on:click={close}
>
    <!-- BACKDROP -->
    <div class="absolute inset-0 bg-black/70"></div>

    <!-- MODAL WINDOW -->
    <div
        class="relative w-[92%] max-w-3xl
               bg-slate-100 border-[6px] border-black
               rounded-2xl shadow-[14px_14px_0_0_#000]
               p-4 md:p-6"
        transition:scale={{ start: 0.9 }}
        on:click|stopPropagation
    >
        <!-- HEADER -->
        <div class="flex justify-between items-center mb-4">
            <h2
                class="text-xl md:text-2xl font-black uppercase"
                style="font-family: 'Silkscreen', cursive;"
            >
                {game.title}
            </h2>

            <button
                on:click={close}
                class="px-3 py-1 text-xs font-black
                       bg-red-500 text-white
                       border-2 border-black
                       shadow-[2px_2px_0_0_#000]"
            >
                CLOSE ✕
            </button>
        </div>

        <!-- MEDIA -->
        <div class="aspect-video bg-black border-4 border-black mb-4 overflow-hidden">
            {#if game.video}
                <video autoplay muted loop playsinline class="w-full h-full object-cover">
                    <source src={game.video} type="video/mp4" />
                </video>
            {:else}
                <img src={game.image} alt={game.title} class="w-full h-full object-cover" />
            {/if}
        </div>

        <!-- DESC -->
        <p class="text-sm md:text-base text-slate-700 mb-4">
            {game.desc}
        </p>

        <!-- TAGS -->
        <div class="flex flex-wrap gap-2">
            {#each game.tags as tag}
                <span
                    class="text-xs font-black uppercase
                           bg-yellow-400 px-2 py-1
                           border-2 border-black
                           shadow-[2px_2px_0_0_#000]"
                >
                    {tag}
                </span>
            {/each}
        </div>
    </div>
</div>
{/if}

<style>
    .line-clamp-3 {
        display: -webkit-box;
        -webkit-line-clamp: 3;
        -webkit-box-orient: vertical;
        overflow: hidden;
    }
</style>
