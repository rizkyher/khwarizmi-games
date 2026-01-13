<script lang="ts">
    import { fade, slide } from 'svelte/transition';

    // State Svelte 5
    let y = $state(0);
    let isScrolled = $derived(y > 20);
    let isMobileOpen = $state(false);

    let navLinks = [
        { name: 'Home', href: '#' },
        { name: 'Games', href: '#games' },
        { name: 'About', href: '#about' },
        { name: 'Team', href: '#team' }
    ];

    function toggleMobile() {
        isMobileOpen = !isMobileOpen;
    }
</script>

<svelte:head>
    <link href="https://fonts.googleapis.com/css2?family=VT323&display=swap" rel="stylesheet">
</svelte:head>

<svelte:window bind:scrollY={y} />

<nav class="fixed top-0 left-0 w-full z-50 transition-all duration-300 font-pixel px-4 {isScrolled ? 'py-2' : 'py-6'}">
    <div class="max-w-7xl mx-auto">
        
        <div class="relative bg-white border-4 border-black p-2 shadow-[8px_8px_0_0_#0C7779] transition-all duration-300 hover:shadow-[6px_6px_0_0_#000] hover:translate-x-[2px] hover:translate-y-[2px]">
            
            <div class="absolute top-1 left-1 w-2 h-2 bg-black opacity-20"></div>
            <div class="absolute top-1 right-1 w-2 h-2 bg-black opacity-20"></div>
            <div class="absolute bottom-1 left-1 w-2 h-2 bg-black opacity-20"></div>
            <div class="absolute bottom-1 right-1 w-2 h-2 bg-black opacity-20"></div>

            <div class="flex justify-between items-center px-2">
                
                <a
    href="/"
    class="logo-container group flex items-center gap-3 relative overflow-hidden p-1"
>
    <div class="w-12 h-12 border-2 border-black bg-white shadow-[2px_2px_0_0_#000] flex items-center justify-center group-hover:translate-x-0.5 group-hover:translate-y-0.5 transition-all">
        <img
            src="/logo.jpg"
            alt="KHWARIZMI Studio"
            class="w-10 h-10 object-contain"
        />
    </div>

    <div class="glitch-layer absolute inset-0 bg-white mix-blend-difference opacity-0 pointer-events-none"></div>
</a>


                <div class="hidden md:flex items-center gap-2">
                    {#each navLinks as link}
                        <a 
                            href={link.href} 
                            class="relative px-6 py-2 text-xl font-bold uppercase tracking-widest text-slate-600 overflow-hidden group/link hover:text-white transition-colors"
                        >
                            <span class="relative z-10">{link.name}</span>
                            <div class="absolute inset-0 bg-[#0C7779] transform -translate-x-full group-hover/link:translate-x-0 transition-transform duration-300 ease-out"></div>
                        </a>
                    {/each}
                </div>

                <div class="flex items-center gap-4">
                    <button class="hidden md:block bg-[#F3E5AB] text-black border-2 border-black px-6 py-2 text-lg font-black uppercase tracking-wide shadow-[4px_4px_0_0_#000] hover:bg-[#0C7779] hover:text-white hover:shadow-[2px_2px_0_0_#000] hover:translate-x-[2px] hover:translate-y-[2px] active:scale-95 transition-all">
                        Let's Talk
                    </button>

                    <button 
                        onclick={toggleMobile}
                        aria-label="Toggle mobile menu"
                        class="md:hidden w-10 h-10 bg-black text-white border-2 border-black flex flex-col items-center justify-center gap-1.5 active:scale-90 transition-transform"
                    >
                        <div class="w-6 h-0.5 bg-white transition-all {isMobileOpen ? 'rotate-45 translate-y-2' : ''}"></div>
                        <div class="w-6 h-0.5 bg-white transition-all {isMobileOpen ? 'opacity-0' : ''}"></div>
                        <div class="w-6 h-0.5 bg-white transition-all {isMobileOpen ? '-rotate-45 -translate-y-2' : ''}"></div>
                    </button>
                </div>
            </div>
        </div>

        {#if isMobileOpen}
            <div 
                transition:slide={{ duration: 300 }}
                class="md:hidden mt-2 bg-black border-4 border-[#F3E5AB] p-4 shadow-[8px_8px_0_0_#0C7779]"
            >
                <div class="flex flex-col gap-2">
                    {#each navLinks as link}
                        <a 
                            href={link.href}
                            onclick={() => isMobileOpen = false} 
                            class="block bg-white/10 text-[#F3E5AB] px-4 py-3 text-2xl font-bold uppercase hover:bg-[#0C7779] hover:text-white border-2 border-transparent hover:border-[#F3E5AB] transition-all"
                        >
                            > {link.name}
                        </a>
                    {/each}
                    <button class="mt-4 w-full bg-[#F3E5AB] text-black border-2 border-black py-3 text-xl font-black uppercase hover:bg-white transition-colors">
                        Contact Us
                    </button>
                </div>
            </div>
        {/if}

    </div>
</nav>

<div class="h-32"></div>

<style>
    .font-pixel {
        font-family: 'VT323', monospace;
    }

    @keyframes glitch {
        0% { transform: translate(0); }
        20% { transform: translate(-2px, 2px); }
        40% { transform: translate(-2px, -2px); }
        60% { transform: translate(2px, 2px); }
        80% { transform: translate(2px, -2px); }
        100% { transform: translate(0); }
    }   

    /* Target hover secara manual agar Svelte mendeteksi selector ini dan tidak error */
    .logo-container:hover .glitch-layer {
        opacity: 0.5;
        animation: glitch 0.2s cubic-bezier(0.25, 0.46, 0.45, 0.94) both infinite;
    }
</style>