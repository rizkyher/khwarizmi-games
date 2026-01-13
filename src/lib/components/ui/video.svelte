<script lang="ts">
    // --- STATE GAME ---
    let score = $state(0);
    let playerPos = $state(45);
    let spirits = $state<{id: number, top: number, left: number}[]>([]);
    let gameStarted = $state(false);

    // --- STATE VIDEO ---
    let videoIndex = $state(0);
    const videos = [
        "https://www.w3schools.com/html/mov_bbb.mp4", 
        "https://www.w3schools.com/html/movie.mp4"
    ];

    let audioCtx: AudioContext;
    const initAudio = () => {
        audioCtx = new (window.AudioContext || (window as any).webkitAudioContext)();
        gameStarted = true;
        playNote(440, "sine", 0.1); 
    };

    const playNote = (freq: number, type: OscillatorType, duration: number) => {
        if (!audioCtx) return;
        const osc = audioCtx.createOscillator();
        const gain = audioCtx.createGain();
        osc.type = type;
        osc.frequency.setValueAtTime(freq, audioCtx.currentTime);
        gain.gain.setValueAtTime(0.1, audioCtx.currentTime);
        gain.gain.exponentialRampToValueAtTime(0.0001, audioCtx.currentTime + duration);
        osc.connect(gain);
        gain.connect(audioCtx.destination);
        osc.start();
        osc.stop(audioCtx.currentTime + duration);
    };

    const move = (e: KeyboardEvent) => {
        if (!gameStarted) return;
        if (e.key === "ArrowLeft" && playerPos > 0) {
            playerPos -= 8;
            playNote(200, "square", 0.05); 
        }
        if (e.key === "ArrowRight" && playerPos < 90) {
            playerPos += 8;
            playNote(250, "square", 0.05); 
        }
    };

    const switchVideo = () => {
        videoIndex = videoIndex === 0 ? 1 : 0;
        playNote(100, "square", 0.1); 
    };

    $effect(() => {
        if (!gameStarted) return;
        const interval = setInterval(() => {
            spirits = spirits.map(s => {
                const newTop = s.top + 2.5;
                if (newTop > 80 && newTop < 92 && Math.abs(s.left - playerPos) < 10) {
                    score += 1;
                    playNote(600 + (score * 5), "triangle", 0.2); 
                    return { ...s, top: 200 }; 
                }
                return { ...s, top: newTop };
            }).filter(s => s.top < 105);
            
            if (Math.random() > 0.93) {
                spirits.push({ id: Math.random(), top: -10, left: Math.random() * 90 });
            }
        }, 30);
        return () => clearInterval(interval);
    });
</script>

<svelte:window onkeydown={move} />

<svelte:head>
    <link href="https://fonts.googleapis.com/css2?family=VT323&display=swap" rel="stylesheet">
</svelte:head>

<div class="game-box relative w-full max-w-xl mx-auto h-[600px] bg-[#0C7779] border-[6px] border-black shadow-[12px_12px_0_0_#000] overflow-hidden font-pixel">
    
    <div class="monitor-screen relative h-1/3 bg-black border-b-[6px] border-black overflow-hidden cursor-crosshair">
        {#key videoIndex}
            <div class="video-wrapper w-full h-full transition-all duration-300">
                <video 
                    src={videos[videoIndex]} 
                    autoplay muted loop 
                    class="video-element w-full h-full object-cover"
                ></video>
            </div>
        {/key}
        
        <div class="teal-tint absolute inset-0 bg-[#0C7779] pointer-events-none transition-opacity duration-300"></div>

        <div class="scanlines pointer-events-none absolute inset-0"></div>

        <div class="monitor-label absolute top-3 left-3 flex items-center gap-2 bg-black/60 px-2 py-1 border border-white/20 transition-all">
            <div class="status-led w-2 h-2 bg-red-600 animate-pulse"></div>
            <span class="text-white text-sm tracking-[0.2em] label-text">REC_CH: 0{videoIndex + 1}</span>
        </div>

        <button 
            onclick={switchVideo}
            class="switch-btn absolute bottom-3 right-3 bg-white border-2 border-black px-3 py-1 text-xs font-bold shadow-[3px_3px_0_0_#000] active:translate-x-1 active:translate-y-1 active:shadow-none transition-all uppercase"
        >
            Signal Switch
        </button>
    </div>

    <div class="relative h-2/3 w-full p-6 bg-[rgba(255,255,255,0.05)]">
        <div class="flex justify-between items-start mb-4">
            <div class="bg-black/20 p-2 border-l-4 border-white transition-all">
                <div class="text-teal-200 text-sm uppercase opacity-70">Extraction_Count</div>
                <div class="text-white font-black text-6xl tabular-nums leading-none">
                    {score.toString().padStart(3, '0')}
                </div>
            </div>
            <div class="text-right">
                <div class="text-[#F3E5AB] text-lg animate-pulse tracking-tighter uppercase">● System Stable</div>
            </div>
        </div>

        <div 
            class="player absolute bottom-12 w-14 h-14 bg-[#F3E5AB] border-4 border-black shadow-[4px_4px_0_0_#000] flex items-center justify-center transition-all duration-75"
            style="left: {playerPos}%"
        >
            <div class="flex gap-2">
                <div class="w-2 h-2 bg-black"></div>
                <div class="w-2 h-2 bg-black"></div>
            </div>
        </div>

        {#each spirits as spirit (spirit.id)}
            <div 
                class="spirit absolute w-8 h-8 bg-white border-2 border-black shadow-[3px_3px_0_0_#0C7779]"
                style="top: {spirit.top}%; left: {spirit.left}%; clip-path: polygon(50% 0%, 100% 50%, 50% 100%, 0% 50%);"
            ></div>
        {/each}
    </div>

    {#if !gameStarted}
        <div class="absolute inset-0 bg-black/95 z-[60] flex flex-col items-center justify-center p-8 text-center">
            <div class="w-16 h-16 bg-[#0C7779] border-4 border-white rotate-45 mb-8 flex items-center justify-center animate-bounce shadow-[0_0_20px_#0C7779]">
                <div class="w-6 h-6 bg-white -rotate-45"></div>
            </div>
            <h2 class="text-white text-5xl font-black mb-2 tracking-tighter uppercase italic">Spirit_Ext.Sys</h2>
            <p class="text-teal-400 text-xl mb-12 font-bold uppercase tracking-widest">Awaiting Manual Override...</p>
            <button 
                onclick={initAudio}
                class="bg-[#F3E5AB] text-black border-4 border-black px-12 py-5 text-3xl font-black shadow-[8px_8px_0_0_#0C7779] hover:bg-white hover:-translate-y-1 active:translate-y-1 transition-all uppercase"
            >
                Start System
            </button>
        </div>
    {/if}
</div>

<style>
    .font-pixel { font-family: 'VT323', monospace; }

    /* --- LOGIKA HOVER MANUAL (VANILLA CSS) --- */
    
    .video-element {
        opacity: 0.3;
        filter: grayscale(1) contrast(1.5);
        transition: all 0.3s ease;
    }

    .teal-tint { opacity: 0; }

    .video-wrapper { animation: glitch 0.3s steps(2) infinite alternate; }

    /* Saat Mouse masuk ke Monitor */
    .monitor-screen:hover .video-element {
        opacity: 0.7;
        filter: grayscale(0) contrast(1.2);
        transform: scale(1.1);
    }

    .monitor-screen:hover .teal-tint {
        opacity: 0.3;
    }

    .monitor-screen:hover .video-wrapper {
        animation-duration: 0.1s; /* Glitch lebih agresif */
    }

    .monitor-screen:hover .status-led {
        background-color: #0C7779;
    }

    .monitor-screen:hover .label-text {
        color: #F3E5AB;
    }

    .monitor-screen:hover .switch-btn {
        box-shadow: 3px 3px 0 0 #0C7779;
        background-color: #F3E5AB;
    }

    /* Efek Scanline */
    .scanlines {
        background: linear-gradient(
            to bottom,
            transparent 50%,
            rgba(0, 0, 0, 0.4) 51%
        );
        background-size: 100% 4px;
        opacity: 0.5;
    }

    .monitor-screen:hover .scanlines {
        background-size: 100% 2px;
        opacity: 0.8;
    }

    @keyframes glitch {
        0% { transform: translate(0); }
        50% { transform: translate(-3px, 2px) skewX(5deg); }
        100% { transform: translate(3px, -2px); }
    }

    .spirit { animation: rotateSpirit 1.5s linear infinite; }
    @keyframes rotateSpirit { from { transform: rotate(0deg); } to { transform: rotate(360deg); } }
    .player { transition: left 0.1s cubic-bezier(0.175, 0.885, 0.32, 1.275); }
</style>