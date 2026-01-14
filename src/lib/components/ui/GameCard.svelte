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
    };

    let open = false;

    function close() {
        open = false;
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

        <button
    on:click={() => window.location.href = game.link}
    class="px-5 py-2 text-sm font-black uppercase
           bg-emerald-400 border-4 border-black
           shadow-[4px_4px_0_0_#000]"
>
    ▶ PLAY GAME
</button>


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
