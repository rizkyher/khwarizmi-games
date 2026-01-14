<script lang="ts">
    import { fade, fly } from 'svelte/transition';
    import { cubicIn } from 'svelte/easing';

    // --- 1. Import Komponen (Pastikan nama file sesuai Besar/Kecilnya) ---
    import Navbar from '$lib/components/ui/Navbar.svelte';
    import Clouds from '$lib/components/ui/Clouds.svelte';
    import Header from '$lib/components/ui/header.svelte'; // Diperbaiki: header -> Header
    import GameCard from '$lib/components/ui/GameCard.svelte';
    import About from '$lib/components/ui/About.svelte';
    import Team from '$lib/components/ui/Team.svelte';
    import Footer from '$lib/components/ui/Footer.svelte';
    import LoadingScreen from '$lib/components/ui/LoadingsScreen.svelte'; 

    // --- 2. Definisi Tipe Data (TypeScript) ---
   interface GameItem {
        id: number;
        title: string;
        desc: string;
        tags: string[];
        color?: string; // Tanda tanya membuatnya tidak wajib
        img: string;
    }

    interface TeamMember {
        name: string;
        role: string;
        avatar: string;
        avatarColor: string;
        bio: string;
    }

    // --- 3. Logika State (Svelte 5 Runes) ---
    let isLoading = $state(true);

    function handleLoadingComplete() {
        isLoading = false;
    }

    // Data Game
    let myGames: Game[] = $state([
        { 
            id: 1, 
            title: "Santri Bros", 
            image: "/SantriBros.png", 
            // Pastikan file ini ada di folder /static/
            video: "", 
            desc: "Petualangan platformer klasik dengan sentuhan lokal santri.", 
            tags: ["Action", "Platformer"] 
        },
        { 
            id: 2, 
            title: "Writing Hijaiyah", 
            image: "https://images.unsplash.com/photo-1506744038136-46273834b3fb?w=600&auto=format&fit=crop&q=60", 
            video: "https://assets.mixkit.co/videos/preview/mixkit-pixel-art-animation-of-a-mountain-landscape-31932-large.mp4",
            desc: "Belajar menulis huruf hijaiyah dengan cara yang menenangkan dan interaktif.", 
            tags: ["Educational", "Cozy"] 
        },
        { 
            id: 3, 
            title: "Flappy Hijaiyah", 
            image: "https://images.unsplash.com/photo-1446776811953-b23d57bd21aa?w=600&auto=format&fit=crop&q=60", 
            video: "https://assets.mixkit.co/videos/preview/mixkit-cartoon-character-running-in-a-forest-41485-large.mp4",
            desc: "Terbang menghindari rintangan sambil mengumpulkan huruf hijaiyah yang tepat.", 
            tags: ["Arcade", "Educational"] 
        },
        { 
            id: 4, 
            title: "Catching Hijaiyah", 
            image: "https://images.unsplash.com/photo-1534234828563-025075d9e54d?w=600&auto=format&fit=crop&q=60", 
            video: "https://assets.mixkit.co/videos/preview/mixkit-pixel-art-of-a-person-running-in-the-rain-31936-large.mp4",
            desc: "Tangkap huruf-huruf hijaiyah yang jatuh sebelum menyentuh tanah.", 
            tags: ["Casual", "Speed"] 
        },
        { 
            id: 5, 
            title: "Car Hijaiyah Hunt", 
            image: "https://images.unsplash.com/photo-1517524008697-84bbe3c3fd98?w=600&auto=format&fit=crop&q=60", 
            video: "https://assets.mixkit.co/videos/preview/mixkit-chef-preparing-food-in-a-kitchen-pixel-art-41490-large.mp4",
            desc: "Berkendara sambil berburu huruf hijaiyah di sepanjang jalanan kota.", 
            tags: ["Racing", "Educational"] 
        },
        { 
            id: 6, 
            title: "Match 3 Hijaiyah", 
            image: "https://images.unsplash.com/photo-1612152605347-f932c6f141d5?w=600&auto=format&fit=crop&q=60", 
            video: "https://assets.mixkit.co/videos/preview/mixkit-starry-night-sky-with-pixel-art-style-clouds-31940-large.mp4",
            desc: "Cocokkan 3 huruf hijaiyah yang sama untuk memecahkan puzzle.", 
            tags: ["Puzzle", "Logic"] 
        }
    ]);

    // Data Team
    let myTeam: TeamMember[] = $state([
        {
            name: "Ucup Markucup",
            role: "Lead Developer",
            avatar: "bayu.png", // Disarankan path absolut dari static
            avatarColor: "bg-blue-200",
            bio: "Spesialis Svelte dan sihir CSS modern."
        },
        {
            name: "Kucai",
            role: "Pixel Artist",
            avatar: "/team/kucai.jpg",
            avatarColor: "bg-rose-200",
            bio: "Menggambar setiap piksel dengan penuh cinta."
        },
        {
            name: "Bujas",
            role: "Game Designer",
            avatar: "/team/bujas.jpg",
            avatarColor: "bg-slate-300",
            bio: "Pakar menciptakan atmosfer menenangkan."
        }
    ]);

    // State Preview
    // Kita inisialisasi dengan data dummy yang aman, atau ambil dari myGames[0]
    let activePreview = $state({
        title: "K H W A R I Z M I",
        video: myGames[1].video 
    });

    function updatePreview(game: Game) {
        activePreview = {
            title: game.title,
            video: game.video
        };
    }
</script>

<svelte:head>
    <link href="https://fonts.googleapis.com/css2?family=Silkscreen:wght@400;700&display=swap" rel="stylesheet">
</svelte:head>

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
                                    <video 
                                        autoplay 
                                        muted 
                                        loop 
                                        playsinline 
                                        class="w-full h-full object-cover opacity-80 group-hover:opacity-100 transition-opacity duration-500"
                                    >
                                        <source src={activePreview.video} type="video/mp4">
                                        Your browser does not support the video tag.
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

               <section
    id="games"
    class="scroll-mt-24 md:scroll-mt-32 overflow-hidden"
>
    <div class="flex flex-col md:flex-row justify-between items-start md:items-end mb-6 md:mb-10 px-2 gap-2 md:gap-0">
        <h2
            class="text-3xl md:text-5xl font-bold text-slate-900 uppercase tracking-wider"
            style="font-family: 'Silkscreen', cursive; text-shadow: 2px 2px 0px #fff, 4px 4px 0px #000;"
        >
            Featured <span class="text-[#0C7779]">Games</span>
        </h2>

        <p
            class="text-[10px] md:text-xs font-bold bg-black text-white px-3 py-1.5 md:px-4 md:py-2 animate-pulse uppercase tracking-widest self-start md:self-auto border-2 border-white shadow-[2px_2px_0_0_#000]"
            style="font-family: 'Silkscreen', cursive;"
        >
            Hover / Focus to Preview | Shift + Scroll →
        </p>
    </div>

    <div
        class="flex overflow-x-auto gap-4 md:gap-8 pb-10 md:pb-14 no-scrollbar snap-x snap-mandatory scroll-smooth px-1"
    >
        {#each myGames as game (game.id)}
           <div
    class="snap-center shrink-0 cursor-pointer"
    onfocusin={() => updatePreview(game)}
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

    /* Utilitas Scrollbar */
    .no-scrollbar::-webkit-scrollbar { display: none; }
    .no-scrollbar { -ms-overflow-style: none; scrollbar-width: none; }

    /* Custom Scrollbar Global */
    :global(::-webkit-scrollbar) { width: 12px; }
    :global(::-webkit-scrollbar-track) { background: #000; }
    :global(::-webkit-scrollbar-thumb) { background: #fbbf24; border: 3px solid #000; }
</style>