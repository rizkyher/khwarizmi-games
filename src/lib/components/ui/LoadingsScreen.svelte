<script lang="ts">
    import { onMount } from 'svelte';

    let { onComplete }: { onComplete: () => void } = $props();

    let progress = $state(0);
    // Teks loading disesuaikan dengan tema "Teal World"
    const phrases = [
        "Initializing Khwarizmi System...",
        "Loading pixel assets...",
        "Calibrating visual core...",
        "Syncing with the cloud...",
        "Welcome to the studio."
    ];
    let loadingText = $state(phrases[0]);

    onMount(() => {
        const interval = setInterval(() => {
            const increment = Math.random() * 2.5 + 0.5; 
            progress = Math.min(progress + increment, 100);

            const phraseIndex = Math.min(
                Math.floor((progress / 100) * phrases.length),
                phrases.length - 1
            );
            loadingText = phrases[phraseIndex];

            if (progress >= 100) {
                clearInterval(interval);
                setTimeout(() => onComplete(), 1500); 
            }
        }, 100); 

        return () => clearInterval(interval);
    });

    // --- DATA PESAWAT TAMBAHAN ---
    // Kita gunakan array untuk mendefinisikan beberapa pesawat dengan properti berbeda
    // agar menciptakan efek parallax (kedalaman).
    const extraPlanes = [
        // Pesawat Asli (Kiri ke Kanan, Sedang)
        { id: 1, direction: 'left', top: '33%', duration: '45s', delay: '0s', scale: 1.0 },
        // Pesawat Baru 1 (Kanan ke Kiri, Atas, Jauh/Kecil, Lambat)
        { id: 2, direction: 'right', top: '15%', duration: '60s', delay: '-15s', scale: 0.6 },
        // Pesawat Baru 2 (Kiri ke Kanan, Bawah, Dekat/Besar, Cepat)
        { id: 3, direction: 'left', top: '55%', duration: '35s', delay: '-5s', scale: 1.3 },
        // Pesawat Baru 3 (Kanan ke Kiri, Tengah, Sedang)
        { id: 4, direction: 'right', top: '40%', duration: '50s', delay: '-30s', scale: 0.8 },
    ];

</script>

<svelte:head>
    <link href="https://fonts.googleapis.com/css2?family=Press+Start+2P&display=swap" rel="stylesheet">
</svelte:head>

<div class="fixed inset-0 z-[9999] overflow-hidden font-['Press_Start_2P'] select-none bg-[#000] text-[#E0F2F1]" style="image-rendering: pixelated;">
    
    <div class="absolute inset-0 bg-[linear-gradient(to_bottom,#085C5E_0%,#4FA4B8_100%)]"></div>
    <div class="absolute top-10 right-20 w-16 h-16 bg-[#FCD34D] border-4 border-[#FBBF24] shadow-[4px_4px_0_rgba(0,0,0,0.2)]"></div>

    <div class="absolute top-20 left-0 right-0 z-40 text-center pointer-events-none">
        <h1 class="text-2xl md:text-4xl text-white drop-shadow-[4px_4px_0_#064042] tracking-widest leading-relaxed">
            P.T. KHWARIZMI
        </h1>
        <div class="mt-2 text-xs md:text-sm text-[#8ED5E7] tracking-[0.5em] uppercase drop-shadow-[2px_2px_0_#064042]">
            Digital Studio
        </div>
    </div>

    <div class="absolute inset-0 opacity-80 animate-drift-slow pointer-events-none">
         <div class="absolute top-32 left-10 w-64 h-24 bg-[#E0F2F1] border-b-8 border-r-8 border-[#B2DFDB]"></div>
         <div class="absolute top-24 left-32 w-48 h-32 bg-[#E0F2F1] border-b-8 border-r-8 border-[#B2DFDB]"></div>
         <div class="absolute top-52 right-[-100px] w-80 h-32 bg-[#E0F2F1] border-b-8 border-r-8 border-[#B2DFDB]"></div>
    </div>
     <div class="absolute inset-0 opacity-50 animate-drift-slower pointer-events-none" style="animation-delay: -20s;">
        <div class="absolute top-72 left-1/2 w-96 h-20 bg-[#B2DFDB] border-b-8 border-r-8 border-[#80CBC4]"></div>
   </div>

    <div class="absolute bottom-0 left-0 right-0 h-64 animate-pan-slow pointer-events-none flex">
        {#each Array(5) as _, i}
        <div class="relative w-screen h-full shrink-0">
             <div class="absolute bottom-0 left-0 w-full h-48 bg-[#0C7779] border-t-8 border-[#149597]" 
                  style="clip-path: polygon(0% 100%, 0% 30%, 20% 10%, 50% 35%, 80% 15%, 100% 40%, 100% 100%);">
            </div>
             <div class="absolute bottom-0 left-[-20%] w-full h-56 bg-[#085C5E] border-t-8 border-[#0A7073] z-[-1]" 
                  style="clip-path: polygon(0% 100%, 10% 40%, 40% 10%, 70% 30%, 100% 20%, 100% 100%);">
            </div>
        </div>
        {/each}
    </div>

    <div class="absolute bottom-0 left-0 right-0 h-32 bg-[#064042] border-t-8 border-[#0C7779] animate-pan-medium pointer-events-none flex items-end">
        {#each Array(20) as _, i}
            <div class="w-4 h-4 bg-[#FCD34D] mx-16 mb-2 border-2 border-[#FBBF24]" style="transform: translateY({i%2===0 ? '0' : '8px'})"></div>
            <div class="w-2 h-6 bg-[#0C7779] mx-4 mb-0"></div>
        {/each}
    </div>


    {#each extraPlanes as plane (plane.id)}
    <div 
        class="absolute z-20 pointer-events-none {plane.direction === 'left' ? 'animate-fly-left' : 'animate-fly-right'}"
        style="
            top: {plane.top}; 
            animation-duration: {plane.duration};
            animation-delay: {plane.delay};
        "
    >
        <div class="relative origin-center" style="transform: scale({plane.scale});">
            <div class="relative w-24 h-10 bg-[#EEEEEE] border-4 border-[#777777] flex items-center justify-center">
                <div class="w-4 h-4 bg-[#E0F2F1] border-2 border-[#777777] mr-1"></div>
                <div class="w-4 h-4 bg-[#E0F2F1] border-2 border-[#777777]"></div>
                <div class="absolute left-[-10px] top-1 w-2 h-8 bg-[#CCCCCC] animate-spin-pixel origin-center"></div>
                <div class="absolute -top-4 right-2 w-12 h-4 bg-[#CCCCCC] border-2 border-[#777777]"></div>
            </div>
        </div>
    </div>
    {/each}


    <div class="absolute bottom-10 left-0 right-0 z-30 flex flex-col items-center px-4">
        <div class="bg-[#064042] border-4 border-[#042B2C] p-6 rounded-none shadow-[8px_8px_0_rgba(0,0,0,0.3)] w-full max-w-md relative">
            <div class="absolute top-1 left-1 w-3 h-3 bg-[#0C7779] border-b-2 border-r-2 border-[#042B2C]"></div>
            <div class="absolute top-1 right-1 w-3 h-3 bg-[#0C7779] border-b-2 border-r-2 border-[#042B2C]"></div>
            <div class="absolute bottom-1 left-1 w-3 h-3 bg-[#0C7779] border-b-2 border-r-2 border-[#042B2C]"></div>
            <div class="absolute bottom-1 right-1 w-3 h-3 bg-[#0C7779] border-b-2 border-r-2 border-[#042B2C]"></div>

            <h2 class="text-sm md:text-lg text-[#E0F2F1] text-center mb-4 leading-relaxed tracking-wider drop-shadow-[2px_2px_0_#042B2C]">
                {loadingText}
            </h2>

             <div class="relative w-full h-8 bg-[#042B2C] border-4 border-[#021819] p-[2px]">
                <div 
                    class="h-full bg-[#0C7779] transition-all duration-300 ease-steps relative"
                    style="width: {progress}%"
                >
                    <div class="absolute top-0 left-0 w-full h-2 bg-[#149597]"></div>
                </div>
             </div>
              <div class="text-right mt-2 text-xs text-[#4FA4B8]">
                 System Status... {Math.floor(progress)}%
             </div>
        </div>
    </div>
</div>

<style>
    /* SEMUA CSS ANIMASI LAINNYA TETAP SAMA */
    .ease-steps {
        transition-timing-function: steps(10, end);
    }

    @keyframes drift {
        from { transform: translateX(0); }
        to { transform: translateX(-50%); }
    }
    .animate-drift-slow {
        animation: drift 120s linear infinite;
        width: 200%;
    }
    .animate-drift-slower {
         animation: drift 180s linear infinite;
         width: 200%;
    }

    @keyframes pan {
        from { transform: translateX(0); }
        to { transform: translateX(-100vw); }
    }
    .animate-pan-slow {
        animation: pan 60s linear infinite;
        width: 200vw;
         display: flex;
    }
    .animate-pan-medium {
        animation: pan 30s linear infinite;
        width: 200vw;
        display: flex;
    }

    /* --- ANIMASI PESAWAT BARU (DIPISAH KIRI & KANAN) --- */

    /* Terbang dari KIRI ke KANAN */
    @keyframes fly-left {
        0% { transform: translateX(-20vw) translateY(0px) rotate(1deg); }
        50% { transform: translateX(50vw) translateY(-15px) rotate(-1deg); }
        100% { transform: translateX(110vw) translateY(0px) rotate(1deg); }
    }
    .animate-fly-left {
        animation-name: fly-left;
        animation-timing-function: linear;
        animation-iteration-count: infinite;
        /* Duration di-set inline di HTML */
    }

    /* Terbang dari KANAN ke KIRI */
    /* PENTING: scaleX(-1) digunakan untuk membalik pesawat agar menghadap kiri */
    @keyframes fly-right {
        0% { transform: translateX(110vw) translateY(0px) rotate(1deg) scaleX(-1); }
        50% { transform: translateX(50vw) translateY(-15px) rotate(-1deg) scaleX(-1); }
        100% { transform: translateX(-20vw) translateY(0px) rotate(1deg) scaleX(-1); }
    }
    .animate-fly-right {
        animation-name: fly-right;
        animation-timing-function: linear;
        animation-iteration-count: infinite;
        /* Duration di-set inline di HTML */
    }

    @keyframes spin-pixel {
        0% { transform: scaleY(1); }
        50% { transform: scaleY(0.2); }
        100% { transform: scaleY(1); }
    }
    .animate-spin-pixel {
        animation: spin-pixel 0.2s steps(2) infinite;
    }
</style>