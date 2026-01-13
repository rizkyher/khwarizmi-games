<script lang="ts">
    import { fade, fly } from 'svelte/transition';
    import { cubicIn } from 'svelte/easing';

    // 1. Import Komponen
    import Navbar from '$lib/components/ui/Navbar.svelte';
    import Clouds from '$lib/components/ui/Clouds.svelte';
    import Header from '$lib/components/ui/header.svelte';
    import GameCard from '$lib/components/ui/GameCard.svelte';
    import About from '$lib/components/ui/About.svelte';
    import Team from '$lib/components/ui/Team.svelte';
    import Footer from '$lib/components/ui/Footer.svelte';
    
    // Pastikan nama file import sesuai (LoadingsScreen atau LoadingScreen)
    import LoadingScreen from '$lib/components/ui/LoadingsScreen.svelte';    

    // --- LOGIKA LOADING SCREEN ---
    let isLoading = $state(true);

    function handleLoadingComplete() {
        isLoading = false;
    }

    // 2. Data Game
   let myGames = $state([
    { 
        id: 1,
        title: "Writing Hijaiyah",
        img: "writing.jpg",
        video: "Video Vario.mp4",
        desc: "Belajar menulis huruf Hijaiyah dengan cara yang menyenangkan.",
        tags: ["Action", "Sci-Fi"]
    },
    { 
        id: 2,
        title: "Spirit Woods",
        img: "/games/spirit-woods.jpg",
        video: "https://assets.mixkit.co/videos/preview/mixkit-pixel-art-animation-of-a-mountain-landscape-31932-large.mp4",
        desc: "Petualangan puzzle santai di dalam hutan yang penuh dengan roh baik.",
        tags: ["Cozy", "Puzzle"]
    },
    { 
        id: 3,
        title: "Sky Castle",
        img: "/games/sky-castle.jpg",
        video: "https://assets.mixkit.co/videos/preview/mixkit-cartoon-character-running-in-a-forest-41485-large.mp4",
        desc: "Bangun kerajaanmu di atas awan dan lindungi dari serangan naga.",
        tags: ["Strategy", "Fantasy"]
    },
    { 
        id: 4,
        title: "Totoro Run",
        img: "/games/totoro-run.jpg",
        video: "https://assets.mixkit.co/videos/preview/mixkit-pixel-art-of-a-person-running-in-the-rain-31936-large.mp4",
        desc: "Lari secepat mungkin untuk mengejar Bus Kucing sebelum hujan turun.",
        tags: ["Runner", "Ghibli"]
    },
    { 
        id: 5,
        title: "Pixel Chef",
        img: "/games/pixel-chef.jpg",
        video: "https://assets.mixkit.co/videos/preview/mixkit-chef-preparing-food-in-a-kitchen-pixel-art-41490-large.mp4",
        desc: "Masak makanan lezat untuk para petualang yang mampir ke kedaimu.",
        tags: ["Simulation"]
    },
    { 
        id: 6,
        title: "Star Gazing",
        img: "/games/star-gazing.jpg",
        video: "https://assets.mixkit.co/videos/preview/mixkit-starry-night-sky-with-pixel-art-style-clouds-31940-large.mp4",
        desc: "Hubungkan rasi bintang untuk mengungkap cerita kuno di langit malam.",
        tags: ["Educational"]
    }
]);


    // 3. State Preview
    let activePreview = $state({
        title: "K H W A R I Z M I",
        video: myGames[1].video 
    });

    function updatePreview(game: any) {
        activePreview = {
            title: game.title,
            video: game.video
        };
    }

    // 4. Data Team
    let myTeam = $state([
    {
        name: "Ucup Markucup",
        role: "Lead Developer",
        avatar: "0.jpg",
        bio: "Spesialis Svelte dan sihir CSS modern."
    },
    {
        name: "Kucai",
        role: "Pixel Artist",
        avatar: "/team/kucai.jpg",
        bio: "Menggambar setiap piksel dengan penuh cinta."
    },
    {
        name: "Bujas",
        role: "Game Designer",
        avatar: "/team/bujas.jpg",
        bio: "Pakar menciptakan atmosfer menenangkan."
    }
]);

</script>

{#if isLoading}
    <div 
        out:fly={{ y: -1500, duration: 1000, easing: cubicIn }} 
        class="fixed inset-0 z-[9999]"
    >
        <LoadingScreen onComplete={handleLoadingComplete} />
    </div>
{/if}

{#if !isLoading}
    <div in:fade={{ duration: 800, delay: 600 }}>
        
        <Clouds />
        <Navbar />

        <main class="relative z-10 min-h-screen">
            <div class="max-w-6xl mx-auto px-4 md:px-6 py-8 md:py-12">
                
                <section id="home">
                    <Header 
                        title="K H W A R I Z M I" 
                        subtitle="Koleksi petualangan kecil dalam balutan pixel art dan estetika Ghibli." 
                    />
                </section>

                <section class="mt-4 md:mt-8 mb-12 md:mb-20 flex flex-col items-center">
                    <div class="relative w-full max-w-3xl group">
                        <div class="absolute -top-4 left-2 md:-top-6 md:left-6 z-20 bg-yellow-400 border-[3px] md:border-4 border-black px-2 md:px-4 py-1 font-black italic uppercase text-[10px] md:text-sm shadow-[3px_3px_0_0_#000] md:shadow-[4px_4px_0_0_#000] -rotate-2">
                            Playing: <span class="truncate max-w-[100px] inline-block align-bottom">{activePreview.title}</span>
                        </div>

                        <div class="bg-slate-800 p-2 md:p-4 pb-8 md:pb-12 rounded-t-[2rem] md:rounded-t-[3rem] border-[4px] md:border-8 border-black shadow-[10px_10px_0_0_rgba(0,0,0,0.2)] md:shadow-[20px_20px_0_0_rgba(0,0,0,0.2)]">
                            <div class="bg-black aspect-video overflow-hidden border-2 md:border-4 border-black relative">
                                {#key activePreview.video}
                                    <video autoplay muted loop playsinline class="w-full h-full object-cover opacity-80 group-hover:opacity-100 transition-opacity duration-500">
                                        <source src={activePreview.video} type="video/mp4">
                                    </video>
                                {/key}

                                <div class="pointer-events-none absolute inset-0 bg-[linear-gradient(rgba(18,16,16,0)_50%,rgba(0,0,0,0.1)_50%),linear-gradient(90deg,rgba(255,0,0,0.02),rgba(0,255,0,0.01),rgba(0,0,255,0.02))] bg-[length:100%_4px,3px_100%]"></div>
                            </div>
                            
                            <div class="absolute bottom-2 md:bottom-4 right-4 md:right-10 flex items-center gap-2">
                                <div class="w-2 h-2 md:w-3 md:h-3 bg-emerald-500 rounded-full animate-pulse shadow-[0_0_10px_#10b981]"></div>
                                <span class="text-[8px] md:text-[10px] text-slate-500 font-bold tracking-widest">SIGNAL OK</span>
                            </div>
                        </div>

                        <div class="w-20 md:w-32 h-4 md:h-6 bg-slate-900 mx-auto border-x-[4px] md:border-x-8 border-black"></div>
                        <div class="w-40 md:w-56 h-3 md:h-4 bg-slate-900 mx-auto border-[4px] md:border-8 border-black rounded-b-lg md:rounded-b-xl"></div>
                    </div>
                </section>

                <div class="my-10 md:my-16 flex justify-center items-center gap-4">
                    <div class="h-1 flex-grow bg-black shadow-[0_2px_0_0_#fff]"></div>
                    <div class="w-3 h-3 md:w-4 md:h-4 bg-yellow-400 border-2 border-black rotate-45"></div>
                    <div class="h-1 flex-grow bg-black shadow-[0_2px_0_0_#fff]"></div>
                </div>

                <section id="games" class="scroll-mt-24 md:scroll-mt-32 overflow-hidden">
                    <div class="flex flex-col md:flex-row justify-between items-start md:items-end mb-6 md:mb-10 px-2 gap-2 md:gap-0">
                        <h2 class="text-2xl md:text-3xl font-black text-slate-800 uppercase italic">
                            Featured <span class="text-blue-600">Games</span>
                        </h2>
                        <p class="text-[9px] md:text-[10px] font-black bg-black text-white px-2 md:px-3 py-1 animate-pulse uppercase tracking-tighter self-start md:self-auto">
                            Hover to Preview | Shift + Scroll →
                        </p>
                    </div>

                    <div class="flex overflow-x-auto gap-4 md:gap-8 pb-10 md:pb-14 no-scrollbar snap-x snap-mandatory scroll-smooth px-1">
                        {#each myGames as game (game.id)}
                            <div 
                                onmouseenter={() => updatePreview(game)} 
                                role="presentation"
                                class="snap-center shrink-0"
                            >
                                <GameCard {game} />
                            </div>
                        {/each}
                    </div>
                </section>

                <section id="about" class="scroll-mt-24 md:scroll-mt-32">
                    <About />
                </section>

                <section id="team" class="scroll-mt-24 md:scroll-mt-32">
                    <Team members={myTeam} />
                </section>

            </div>

            <Footer creator="P.T. KHWARIZMI" />
        </main>
    </div>
{/if}

<style>
    @import url('https://fonts.googleapis.com/css2?family=DotGothic16&display=swap');

    :global(html) { scroll-behavior: smooth; }

    :global(body) {
        margin: 0; padding: 0;
        font-family: 'DotGothic16', sans-serif;
        background: linear-gradient(to bottom, #bae6fd 0%, #e0f2fe 50%, #f0f9ff 100%);
        color: #1e293b;
        overflow-x: hidden;
    }

    .no-scrollbar::-webkit-scrollbar { display: none; }
    .no-scrollbar { -ms-overflow-style: none; scrollbar-width: none; }

    :global(::-webkit-scrollbar) { width: 12px; }
    :global(::-webkit-scrollbar-track) { background: #000; }
    :global(::-webkit-scrollbar-thumb) { background: #fbbf24; border: 3px solid #000; }
</style>