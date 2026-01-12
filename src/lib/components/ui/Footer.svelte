<script lang="ts">
    // Kita bisa menambahkan props jika ingin custom teks
    let { creator = "YourName" } = $props();
    
    const year = new Date().getFullYear();
</script>

<footer class="relative mt-32 w-full">
    <div class="absolute -top-8 left-0 w-full h-8 flex items-end overflow-hidden pointer-events-none">
        {#each Array(20) as _}
            <div class="flex-1 h-4 bg-emerald-500 border-t-4 border-l-4 border-black" 
                 style="height: {Math.random() * 20 + 10}px"></div>
            <div class="flex-1 h-6 bg-emerald-400 border-t-4 border-l-4 border-black"></div>
        {/each}
    </div>

    <div class="bg-emerald-600 border-t-8 border-black p-10">
        <div class="max-w-6xl mx-auto flex flex-col md:flex-row justify-between items-center gap-8">
            
            <div class="text-white space-y-2">
                <div class="flex items-center gap-3">
                    <div class="w-10 h-10 bg-white border-4 border-black flex items-center justify-center shadow-[4px_4px_0_0_#000]">
                        <div class="w-4 h-4 bg-black animate-bounce"></div>
                    </div>
                    <h2 class="text-2xl font-black uppercase tracking-tighter">Pixel Studio</h2>
                </div>
                <p class="text-emerald-100 font-medium italic">© {year} {creator}. All rights reserved.</p>
            </div>

            <div class="flex gap-4">
                {#each ['Github', 'Itch.io', 'Twitter'] as platform}
                    <a 
                        href="#{platform}" 
                        class="px-4 py-2 bg-white border-4 border-black font-bold text-sm uppercase shadow-[4px_4px_0_0_#000] hover:translate-x-1 hover:translate-y-1 hover:shadow-none transition-all"
                    >
                        {platform}
                    </a>
                {/each}
            </div>
        </div>

        <div class="mt-12 text-center">
            <div class="inline-block bg-black/20 px-4 py-2 rounded-full">
                <p class="text-[10px] text-emerald-100 font-bold uppercase tracking-widest">
                    Forged with <span class="text-red-400">❤</span> using Svelte 5 & Tailwind v4
                </p>
            </div>
        </div>
    </div>
</footer>

<style>
    /* Tambahan font jika belum ada */
    footer {
        font-family: 'DotGothic16', sans-serif;
    }
</style>