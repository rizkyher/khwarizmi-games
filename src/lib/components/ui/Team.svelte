<script lang="ts">
    interface Member {
        name: string;
        role: string;
        avatarColor: string;
        avatar: string; // Tambahkan avatar string
        bio: string;
        longBio?: string;
    }

    let { members }: { members: Member[] } = $props();

    let isModalOpen = $state(false);
    let selectedMember = $state<Member | null>(null);

    function openModal(member: Member) {
        selectedMember = member;
        isModalOpen = true;
        if (typeof document !== 'undefined') document.body.style.overflow = 'hidden';
    }

    function closeModal() {
        isModalOpen = false;
        if (typeof document !== 'undefined') document.body.style.overflow = 'auto';
    }

    function handleKeydown(event: KeyboardEvent) {
        if (event.key === 'Escape' && isModalOpen) {
            closeModal();
        }
    }
</script>

<svelte:window onkeydown={handleKeydown} />

<svelte:head>
    <link href="https://fonts.googleapis.com/css2?family=Silkscreen:wght@400;700&display=swap" rel="stylesheet">
</svelte:head>

<section id="team" class="py-24 max-w-6xl mx-auto px-6 font-silkscreen">
    
    <div class="text-center mb-24">
        <div class="relative inline-block group">
            <h2 class="section-title text-5xl md:text-7xl font-bold text-white uppercase tracking-wider relative z-10 
                       bg-[#0C7779] border-4 border-black px-8 py-4 shadow-[8px_8px_0_0_#000]
                       group-hover:-translate-y-2 group-hover:shadow-[12px_12px_0_0_#FCD34D] 
                       transition-all duration-200 cursor-default"
                style="text-shadow: 4px 4px 0px #000;">
                The Creators
                
                <div class="absolute inset-0 pointer-events-none opacity-0 group-hover:opacity-100">
                    <div class="pixel-dust d1"></div>
                    <div class="pixel-dust d2"></div>
                    <div class="pixel-dust d3"></div>
                    <div class="pixel-dust d4"></div>
                </div>
            </h2>
            <div class="absolute inset-0 bg-black translate-x-4 translate-y-4 -z-10 group-hover:translate-x-6 group-hover:translate-y-6 transition-transform"></div>
        </div>
    </div>

    <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-12">
        {#each members as member}
            <button 
                onclick={() => openModal(member)}
                class="group text-left bg-white border-4 border-black p-6 shadow-[8px_8px_0_0_#0C7779] 
                       hover:shadow-[12px_12px_0_0_#000] hover:-translate-x-1 hover:-translate-y-1 
                       transition-all duration-300 outline-none relative overflow-hidden"
            >
                <div class="w-full aspect-square border-4 border-black mb-6 relative overflow-hidden flex items-center justify-center bg-slate-100 shadow-[4px_4px_0_0_rgba(0,0,0,0.2)]">
                    
                    {#if member.avatar && !member.avatar.endsWith('0.jpg')}
                         <img
                            src={member.avatar}
                            alt={member.name}
                            class="absolute inset-0 w-full h-full object-cover transition-transform duration-300 group-hover:scale-110"
                            loading="lazy"
                        />
                    {:else}
                        <div class="w-full h-full bg-[#0C7779] flex items-center justify-center text-white text-6xl">
                            {member.name.charAt(0)}
                        </div>
                    {/if}

                    <div class="absolute inset-0 pointer-events-none opacity-10 bg-[radial-gradient(#000_2px,transparent_1px)] [background-size:4px_4px]"></div>
                </div>

                <div class="text-center relative z-10">
                    <h3 class="text-2xl md:text-3xl font-bold uppercase text-black leading-tight group-hover:text-[#0C7779] transition-colors"
                        style="text-shadow: 2px 2px 0px #eee;">
                        {member.name}
                    </h3>
                    
                    <div class="mt-3 inline-block bg-black text-[#FCD34D] font-bold text-sm md:text-base tracking-widest uppercase px-3 py-1 border-2 border-black shadow-[3px_3px_0_0_#0C7779]">
                        {member.role}
                    </div>
                    
                    <p class="text-slate-600 text-sm md:text-base font-sans font-bold leading-tight italic pt-4 mt-4 border-t-2 border-black/10">
                        "{member.bio}"
                    </p>
                </div>
            </button>
        {/each}
    </div>
</section>

{#if isModalOpen && selectedMember}
    <div 
        class="fixed inset-0 z-[100] flex items-center justify-center p-6 bg-black/90 backdrop-blur-sm font-silkscreen"
        onclick={closeModal}
        onkeydown={(e) => e.key === 'Enter' && closeModal()}
        role="button"
        tabindex="0"
        aria-label="Close modal overlay"
    >
        <div 
            class="bg-[#E0F2FE] border-[6px] border-black w-full max-w-3xl shadow-[16px_16px_0_0_#0C7779] animate-modal-pop relative overflow-hidden"
            onclick={(e) => e.stopPropagation()}
            onkeydown={(e) => e.stopPropagation()}
            role="dialog"
            aria-modal="true"
            tabindex="-1" 
        >
            <button 
                onclick={closeModal}
                class="absolute top-4 right-4 w-10 h-10 bg-red-500 border-4 border-black text-white font-bold text-xl flex items-center justify-center shadow-[4px_4px_0_0_#000] hover:scale-110 active:scale-95 transition-transform z-50 hover:bg-red-600"
                aria-label="Close modal"
            >
                X
            </button>

            <div class="absolute inset-0 opacity-10 pointer-events-none" 
                 style="background-image: linear-gradient(#0C7779 1px, transparent 1px), linear-gradient(90deg, #0C7779 1px, transparent 1px); background-size: 20px 20px;">
            </div>

            <div class="p-8 md:p-10 flex flex-col md:flex-row gap-8 relative z-10">
                
                <div class="w-full md:w-5/12 aspect-square border-4 border-black relative overflow-hidden bg-white shadow-[8px_8px_0_0_rgba(0,0,0,0.8)] rotate-[-2deg]">
                    {#if selectedMember.avatar && !selectedMember.avatar.endsWith('0.jpg')}
                        <img
                            src={selectedMember.avatar}
                            alt={selectedMember.name}
                            class="absolute inset-0 w-full h-full object-cover"
                        />
                    {:else}
                         <div class="w-full h-full bg-[#0C7779] flex items-center justify-center text-white text-8xl">
                            {selectedMember.name.charAt(0)}
                        </div>
                    {/if}
                    <div class="absolute inset-0 pointer-events-none opacity-20 bg-[radial-gradient(#000_2px,transparent_1px)] [background-size:6px_6px]"></div>
                </div>

                <div class="flex-1 space-y-5 text-left flex flex-col justify-center">
                    <div>
                        <h2 class="text-4xl md:text-5xl font-bold uppercase text-[#0C7779] leading-none" style="text-shadow: 3px 3px 0px #000;">
                            {selectedMember.name}
                        </h2>
                        <div class="mt-2 inline-block bg-[#FCD34D] border-2 border-black px-3 py-1 text-sm font-bold uppercase tracking-widest text-black shadow-[3px_3px_0_0_#000]">
                            {selectedMember.role}
                        </div>
                    </div>
                    
                    <div class="h-1 w-full bg-black/20 rounded-full"></div>
                    
                    <p class="text-lg md:text-xl text-slate-800 leading-snug font-sans font-bold">
                        "{selectedMember.longBio || selectedMember.bio}"
                    </p>
                    
                    <button class="self-start mt-4 px-6 py-3 bg-black text-white border-4 border-transparent font-bold uppercase tracking-wider shadow-[4px_4px_0_0_#0C7779] hover:bg-[#0C7779] hover:text-white hover:border-black hover:shadow-[4px_4px_0_0_#000] hover:-translate-y-1 transition-all">
                        View Portfolio →
                    </button>
                </div>
            </div>
        </div>
    </div>
{/if}

<style>
    .font-silkscreen { font-family: 'Silkscreen', cursive; }

    /* Pixel Dust Animation */
    .pixel-dust {
        position: absolute; width: 8px; height: 8px;
        background: #FCD34D; border: 2px solid black;
    }

    .group:hover .d1 { animation: dust-float-1 0.6s infinite; }
    .group:hover .d2 { animation: dust-float-2 0.7s infinite; }
    .group:hover .d3 { animation: dust-float-3 0.8s infinite; }
    .group:hover .d4 { animation: dust-float-4 0.5s infinite; }

    @keyframes dust-float-1 { 0% { transform: translate(0, 0); opacity: 1; } 100% { transform: translate(-40px, -60px) rotate(45deg); opacity: 0; } }
    @keyframes dust-float-2 { 0% { transform: translate(0, 0); opacity: 1; } 100% { transform: translate(50px, -70px) rotate(-45deg); opacity: 0; } }
    @keyframes dust-float-3 { 0% { transform: translate(0, 0); opacity: 1; } 100% { transform: translate(-60px, 40px) rotate(90deg); opacity: 0; } }
    @keyframes dust-float-4 { 0% { transform: translate(0, 0); opacity: 1; } 100% { transform: translate(70px, 50px) rotate(-90deg); opacity: 0; } }

    /* Modal Animation */
    @keyframes modalPop {
        0% { transform: scale(0.8) translateY(20px); opacity: 0; }
        100% { transform: scale(1) translateY(0); opacity: 1; }
    }
    .animate-modal-pop { animation: modalPop 0.3s cubic-bezier(0.34, 1.56, 0.64, 1) forwards; }
</style>