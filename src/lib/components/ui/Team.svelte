<script lang="ts">
    interface Member {
        name: string;
        role: string;
        avatarColor: string;
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

    // Handler untuk menutup modal dengan keyboard (Escape)
    function handleKeydown(event: KeyboardEvent) {
        if (event.key === 'Escape' && isModalOpen) {
            closeModal();
        }
    }
</script>

<svelte:window onkeydown={handleKeydown} />

<svelte:head>
    <link href="https://fonts.googleapis.com/css2?family=VT323&display=swap" rel="stylesheet">
</svelte:head>

<section id="team" class="py-24 max-w-6xl mx-auto px-6 font-pixel">
    <div class="text-center mb-24">
        <div class="relative inline-block group">
            <h2 class="section-title text-7xl font-black text-white uppercase tracking-tighter relative z-10 
                       bg-[#0C7779] border-4 border-black px-8 py-2 shadow-[8px_8px_0_0_#000]
                       group-hover:-translate-y-2 group-hover:shadow-[12px_12px_0_0_#F3E5AB] 
                       active:scale-90 transition-all duration-200 cursor-default">
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

    <div
  class="flex gap-12 overflow-x-auto snap-x snap-mandatory
         pb-8 px-2
         touch-pan-x scroll-smooth hide-scrollbar"
>

        {#each members as member}
<button 
    onclick={() => openModal(member)}
    class="group shrink-0 snap-center
           w-[320px]
           text-left bg-[#0C7779] border-4 border-black p-6
           shadow-[10px_10px_0_0_#000]
           hover:shadow-[12px_12px_0_0_#F3E5AB]
           hover:-translate-x-1 hover:-translate-y-1
           transition-all duration-300 outline-none
           hover-wiggle"
>

                <div class="w-full aspect-square border-4 border-black mb-6 relative overflow-hidden flex items-center justify-center shadow-[4px_4px_0_0_#000] bg-white">
    
    <img
        src={member.avatar}
        alt={member.name}
        class="absolute inset-0 w-full h-full object-cover transition-transform duration-300 group-hover:scale-105"
        loading="lazy"
    />

    <!-- overlay pixel / texture -->
    <div class="absolute inset-0 pointer-events-none opacity-20
                bg-[radial-gradient(#000_2px,transparent_1px)]
                [background-size:6px_6px]">
    </div>

    <!-- optional blush overlay (ganti mata pixel) -->

</div>


                <div class="text-center">
                    <h3 class="text-4xl font-black uppercase text-white leading-none group-hover:text-[#F3E5AB] transition-colors">
                        {member.name}
                    </h3>
                    <p class="mt-3 bg-[#F3E5AB] text-[#0C7779] font-bold text-lg tracking-widest uppercase inline-block px-3 py-0.5 border-2 border-black shadow-[3px_3px_0_0_#000]">
                        {member.role}
                    </p>
                    <p class="text-teal-50 text-xl leading-tight italic pt-5 border-t-2 border-white/20 mt-4">
                        "{member.bio}"
                    </p>
                </div>
            </button>
        {/each}
    </div>
</section>

{#if isModalOpen && selectedMember}
    <div 
        class="fixed inset-0 z-[100] flex items-center justify-center p-6 bg-black/80 backdrop-blur-sm"
        onclick={closeModal}
        onkeydown={(e) => e.key === 'Enter' && closeModal()}
        role="button"
        tabindex="0"
        aria-label="Close modal overlay"
    >
        <div 
            class="bg-white border-8 border-black w-full max-w-2xl shadow-[16px_16px_0_0_#0C7779] animate-modal-pop relative"
            onclick={(e) => e.stopPropagation()}
            onkeydown={(e) => e.stopPropagation()}
            role="dialog"
            aria-modal="true"
            tabindex="-1" 
        >
            <button 
                onclick={closeModal}
                class="absolute -top-6 -right-6 w-12 h-12 bg-red-500 border-4 border-black text-white font-black text-2xl shadow-[4px_4px_0_0_#000] hover:scale-110 active:scale-90 transition-transform z-50"
                aria-label="Close modal"
            >
                X
            </button>

            <div class="p-8 md:p-12 flex flex-col md:flex-row gap-8">
                <div class="w-full md:w-1/3 aspect-square border-4 border-black relative overflow-hidden bg-white shadow-[6px_6px_0_0_#000]">
    
    <img
        src={selectedMember.avatar}
        alt={selectedMember.name}
        class="absolute inset-0 w-full h-full object-cover"
        loading="lazy"
    />

    <!-- overlay pixel optional -->
    <div class="absolute inset-0 pointer-events-none opacity-20
                bg-[radial-gradient(#000_2px,transparent_1px)]
                [background-size:6px_6px]">
    </div>
</div>


                <div class="flex-1 space-y-4">
                    <h2 class="text-5xl font-black uppercase text-[#0C7779]">{selectedMember.name}</h2>
                    <div class="bg-black text-[#F3E5AB] inline-block px-4 py-1 text-xl font-bold uppercase tracking-wider">
                        {selectedMember.role}
                    </div>
                    <div class="h-1 w-full bg-slate-200"></div>
                    <p class="text-2xl text-slate-700 leading-tight italic">
                        "{selectedMember.longBio || selectedMember.bio}"
                    </p>
                    
                    <button class="mt-4 px-6 py-2 bg-[#0C7779] text-white border-2 border-black font-bold uppercase shadow-[4px_4px_0_0_#000] hover:translate-x-1 hover:translate-y-1 hover:shadow-none transition-all">
                        Follow Work
                    </button>
                </div>
            </div>
        </div>
    </div>
{/if}

<style>
    .font-pixel { font-family: 'VT323', monospace; }

    .pixel-dust {
        position: absolute; width: 8px; height: 8px;
        background: #F3E5AB; border: 2px solid black;
    }

    .group:hover .d1 { animation: dust-float-1 0.6s infinite; }
    .group:hover .d2 { animation: dust-float-2 0.7s infinite; }
    .group:hover .d3 { animation: dust-float-3 0.8s infinite; }
    .group:hover .d4 { animation: dust-float-4 0.5s infinite; }

    @keyframes dust-float-1 { 0% { transform: translate(0, 0); opacity: 1; } 100% { transform: translate(-40px, -60px) rotate(45deg); opacity: 0; } }
    @keyframes dust-float-2 { 0% { transform: translate(0, 0); opacity: 1; } 100% { transform: translate(50px, -70px) rotate(-45deg); opacity: 0; } }
    @keyframes dust-float-3 { 0% { transform: translate(0, 0); opacity: 1; } 100% { transform: translate(-60px, 40px) rotate(90deg); opacity: 0; } }
    @keyframes dust-float-4 { 0% { transform: translate(0, 0); opacity: 1; } 100% { transform: translate(70px, 50px) rotate(-90deg); opacity: 0; } }

    @keyframes eyeBlink { 0%, 90%, 100% { transform: scaleY(1); } 95% { transform: scaleY(0.1); } }
    .animate-eye-blink { animation: eyeBlink 4s infinite; }

    @keyframes modalPop {
        0% { transform: scale(0.5); opacity: 0; }
        70% { transform: scale(1.05); }
        100% { transform: scale(1); opacity: 1; }
    }
    .animate-modal-pop { animation: modalPop 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275) forwards; }

    section { animation: slideUp 0.8s cubic-bezier(0.175, 0.885, 0.32, 1.275); }
    @keyframes slideUp { from { opacity: 0; transform: translateY(30px); } to { opacity: 1; transform: translateY(0); } }
</style>