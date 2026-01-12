<script lang="ts">
	// Definisi struktur data game
	interface GameItem {
		id: number;
		title: string;
		desc: string;
		tags: string[];
		color: string;
	}

	let { game }: { game: GameItem } = $props();
	
	// State lokal untuk efek hover menggunakan Runes
	let isHovered = $state(false);
</script>

<div 
	onmouseenter={() => isHovered = true}
	onmouseleave={() => isHovered = false}
	role="button"
	tabindex="0"
	class="group relative bg-white border-4 border-black p-2 transition-transform hover:-translate-y-2 cursor-pointer shadow-[8px_8px_0_0_#000]"
>
	<div class="aspect-video {game.color} border-4 border-black flex items-center justify-center relative overflow-hidden">
		<span class="text-white font-black text-2xl drop-shadow-[2px_2px_0_#000]">PREVIEW</span>
		
		{#if isHovered}
			<div class="absolute inset-0 bg-yellow-300/40 flex items-center justify-center backdrop-blur-[2px]">
				<span class="bg-white border-2 border-black px-4 py-1 font-bold">PLAY GAME</span>
			</div>
		{/if}
	</div>

	<div class="p-4">
		<h2 class="text-2xl font-bold text-slate-900 uppercase mb-2">{game.title}</h2>
		<p class="text-slate-600 text-sm mb-4 line-clamp-2">{game.desc}</p>
		
		<div class="flex gap-2 flex-wrap">
			{#each game.tags as tag}
				<span class="bg-slate-100 border-2 border-black px-2 py-0.5 text-[10px] font-bold uppercase">
					{tag}
				</span>
			{/each}
		</div>
	</div>
</div>