<script lang="ts">
    interface GameItem {
        id: number;
        title: string;
        desc: string;
        tags: string[];
        image: string; // Updated from 'color' to 'image'
        video?: string;
    }

    let { game }: { game: GameItem } = $props();
    
    let isHovered = $state(false);
    let isModalOpen = $state(false);

    const toggleModal = () => {
        isModalOpen = !isModalOpen;
        if (typeof window !== 'undefined') {
            document.body.style.overflow = isModalOpen ? 'hidden' : 'auto';
        }
    };

    // Handler untuk menutup modal dengan tombol Escape
    const handleKeydown = (e: KeyboardEvent) => {
        if (isModalOpen && e.key === 'Escape') {
            toggleModal();
        }
    };
</script>

<svelte:window onkeydown={handleKeydown} />

<svelte:head>
    <link href="https://fonts.googleapis.com/css2?family=VT323&display=swap" rel="stylesheet">
</svelte:head>

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

            <div class="absolute inset-0 opacity-20 bg-[radial-gradient(#000_2px,transparent_1px)] [background-size:6px_6px] pointer-events-none"></div>

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


        <div class="p-3 md:p-4 bg-white transition-colors">
            <h2 class="text-xl md:text-2xl font-black text-slate-900 uppercase mb-2 group-hover:text-[#0C7779] transition-colors leading-none truncate">
                {game.title}
            </h2>
            <div class="flex gap-2 flex-wrap">
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
                        >
                            PLAY NOW →
                        </button>
                    </div>

                </div>
            </div>
        </div>
    </div>
{/if}

<style>
    :global(.font-pixel) {
        font-family: 'VT323', monospace;
    }

    .animate-modal-in {
        animation: modalShow 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275) forwards;
    }

    .animate-fade {
        animation: fadeIn 0.2s ease-out;
    }

    @keyframes modalShow {
        from { transform: scale(0.9) translateY(50px); opacity: 0; }
        to { transform: scale(1) translateY(0); opacity: 1; }
    }

    @keyframes fadeIn {
        from { opacity: 0; }
        to { opacity: 1; }
    }
</style>