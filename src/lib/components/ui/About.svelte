<script lang="ts">
    // Data awan dengan variasi durasi dan skala untuk efek kedalaman (Parallax)
    const cloudLayers = [
        { top: '10%', duration: '40s', scale: '0.9', opacity: '0.6', delay: '0s' },
        { top: '25%', duration: '25s', scale: '1.5', opacity: '0.8', delay: '-5s' },
        { top: '45%', duration: '50s', scale: '1.2', opacity: '0.5', delay: '-10s' },
        { top: '70%', duration: '30s', scale: '2.0', opacity: '0.7', delay: '-15s' },
        { top: '85%', duration: '60s', scale: '0.8', opacity: '0.6', delay: '-20s' }
    ];
</script>

<div class="fixed inset-0 pointer-events-none overflow-hidden z-[-1] bg-[#eef7f7]">
    {#each cloudLayers as cloud}
        <div 
            class="absolute animate-drift will-change-transform"
            style="
                top: {cloud.top}; 
                /* Posisi awal responsif: lebih dekat di HP (-200px), lebih jauh di Desktop (-400px) */
                left: -200px;
                animation-duration: {cloud.duration}; 
                animation-delay: {cloud.delay};
                opacity: {cloud.opacity};
                --base-scale: {cloud.scale};
            "
        >
            <div class="transform scale-[0.6] md:scale-100 transition-transform duration-300 origin-center">
                
                <div class="relative scale-[var(--base-scale)]">
                    
                    <div class="relative w-44 h-14 bg-[#0C7779] shadow-[6px_6px_0_0_#065a5b]">
                        <div class="absolute -top-8 left-8 w-16 h-16 bg-[#0C7779]"></div>
                        <div class="absolute -top-6 left-20 w-20 h-12 bg-[#0C7779]"></div>
                        <div class="absolute top-4 -left-6 w-14 h-10 bg-[#0C7779]"></div>
                        
                        <div class="absolute top-0 left-0 w-full h-2 bg-white/10"></div>
                        <div class="absolute bottom-0 left-0 w-full h-3 bg-black/20"></div>
                    </div>
                    
                    <div class="absolute top-4 left-4 w-44 h-14 bg-black/5 -z-10 translate-x-2 translate-y-2"></div>
                </div>

            </div>
        </div>
    {/each}
</div>

<style>
    @media (min-width: 768px) {
        .animate-drift {
            left: -400px !important;
        }
    }

    @keyframes drift {
        from { transform: translateX(0); }
        to { transform: translateX(calc(100vw + 400px)); }
    }

    .animate-drift {
        animation: drift linear infinite;
        filter: blur(0.5px);
    }
</style>