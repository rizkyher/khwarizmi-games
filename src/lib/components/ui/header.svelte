<script lang="ts">
    interface Props {
        title: string;
        subtitle: string;
    }

    let { title, subtitle }: Props = $props();

    // Partikel debu acak
    const particles = Array.from({ length: 12 }, (_, i) => ({
        id: i,
        top: Math.random() * 100 + '%',
        left: Math.random() * 100 + '%',
        delay: Math.random() * 5 + 's',
        duration: 4 + Math.random() * 4 + 's',
        size: Math.random() * 4 + 2 + 'px'
    }));
</script>

<style>
    @import url('https://fonts.googleapis.com/css2?family=Press+Start+2P&display=swap');

    .pixel-font {
        font-family: 'Press Start 2P', cursive;
        image-rendering: pixelated;
        line-height: 1.4;
        transition: all 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275);
        cursor: pointer;
        display: inline-block;
    }

    /* --- PERUBAHAN WARNA INTERAKSI DI SINI --- */
    
    /* 1. Efek Hover Judul (Menjadi Hijau #41B78E) */
    @media (hover: hover) {
        .pixel-font:hover {
            color: #41B78E; /* Warna Hijau Baru */
            transform: scale(1.05) rotate(-1deg);
            text-shadow: 4px 4px 0px #000;
        }

        /* 2. Efek Hover Garis Bawah (Menjadi Orange #F9BA72) */
        .pixel-font:hover + .underline-box {
            background-color: #F9BA72; /* Warna Orange Baru */
            transform: translateY(5px);
            box-shadow: none; 
            border-color: #000;
        }
        
        /* 3. Efek Hover Partikel (Berubah jadi Hijau) */
        .header-container:hover .dust-particle {
            background-color: #41B78E;
            filter: brightness(1.1);
        }
    }

    /* 4. Efek Debu Default (Warna Orange #F9BA72 - Seperti serbuk emas) */
    .dust-particle {
        position: absolute;
        background-color: #F9BA72; /* Warna Orange Baru */
        pointer-events: none;
        z-index: 1;
        animation: dustFloat var(--dur) ease-in-out infinite;
    }

    /* KEYFRAMES */
    @keyframes dustFloat {
        0% { transform: translate(0, 0); opacity: 0; }
        20% { opacity: 0.6; }
        50% { transform: translate(20px, -30px); }
        100% { transform: translate(40px, -60px); opacity: 0; }
    }

    @keyframes textFloat {
        0%, 100% { transform: translateY(0); }
        50% { transform: translateY(-8px); }
    }

    @keyframes fadeIn {
        from { opacity: 0; filter: blur(5px); }
        to { opacity: 1; filter: blur(0); }
    }

    .animate-text-float {
        animation: textFloat 4s ease-in-out infinite;
    }

    .animate-entry {
        animation: fadeIn 1s ease-out forwards;
    }

    .underline-box {
        transition: all 0.3s ease;
        box-shadow: 3px 3px 0 0 #000;
    }
    
    @media (min-width: 768px) {
        .underline-box {
            box-shadow: 4px 4px 0 0 #000;
        }
    }
</style>

<header class="text-center mb-10 md:mb-16 mt-6 md:mt-10 p-6 md:p-10 header-container overflow-hidden w-full px-4">
    
    <div class="inline-block relative animate-entry max-w-full">
        {#each particles as p}
            <div 
                class="dust-particle hidden sm:block" 
                style="
                    top: {p.top}; 
                    left: {p.left}; 
                    width: {p.size}; 
                    height: {p.size}; 
                    animation-delay: {p.delay};
                    --dur: {p.duration};
                "
            ></div>
        {/each}

        <div class="animate-text-float relative z-10 px-2">
            <h1 class="pixel-font text-2xl sm:text-3xl md:text-5xl text-slate-800 mb-2 md:mb-4 tracking-tighter uppercase relative z-20 break-words leading-relaxed">
                {title}
            </h1>
            
            <div class="underline-box h-1.5 md:h-2 w-full bg-[#41B78E] border-[2px] md:border-[3px] border-black absolute -bottom-1 md:-bottom-2 left-0"></div>
        </div>
    </div>
    
    {#if subtitle}
        <p class="mt-6 md:mt-10 text-slate-600 text-[10px] md:text-xs font-bold uppercase tracking-[0.2em] md:tracking-[0.4em] opacity-0 animate-[fadeIn_1s_ease-out_forwards] [animation-delay:0.8s] px-4 leading-relaxed">
            {subtitle}
        </p>
    {/if}
</header>

<hr class="border-t-2 border-[#F9BA72]/30 mx-auto w-3/4 md:w-1/2" />