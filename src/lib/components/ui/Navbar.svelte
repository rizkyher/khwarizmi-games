<script lang="ts">
	// Svelte 5 state untuk mendeteksi scroll
	let y = $state(0);
	let isScrolled = $derived(y > 50);

	let navLinks = [
		{ name: 'Home', href: '#' },
		{ name: 'Games', href: '#games' },
		{ name: 'About', href: '#about' }
	];
</script>

<svelte:window bind:scrollY={y} />

<nav class="fixed top-0 left-0 w-full z-50 transition-all duration-300 {isScrolled ? 'py-2' : 'py-6'}">
	<div class="max-w-6xl mx-auto px-6">
		<div class="bg-white/80 backdrop-blur-md border-4 border-black p-3 shadow-[6px_6px_0_0_#000] flex justify-between items-center transition-all">
			
			<a href="/" class="flex items-center gap-2 group">
				<div class="w-8 h-8 bg-blue-400 border-2 border-black flex items-center justify-center group-hover:rotate-12 transition-transform">
					<div class="w-2 h-2 bg-white animate-pulse"></div>
				</div>
				<span class="font-black text-xl tracking-tighter text-slate-800">PIXEL.STUDIO</span>
			</a>

			<div class="hidden md:flex gap-8">
				{#each navLinks as link}
					<a 
						href={link.href} 
						class="font-bold text-sm uppercase tracking-widest text-slate-600 hover:text-blue-500 transition-colors relative group"
					>
						{link.name}
						<span class="absolute -bottom-1 left-0 w-0 h-1 bg-yellow-400 transition-all group-hover:w-full"></span>
					</a>
				{/each}
			</div>

			<button class="bg-emerald-500 text-white border-2 border-black px-4 py-1 text-xs font-bold uppercase shadow-[3px_3px_0_0_#000] hover:translate-x-[2px] hover:translate-y-[2px] hover:shadow-none transition-all active:scale-95">
				Contact
			</button>
		</div>
	</div>
</nav>

<div class="h-24"></div>

<style>
	nav {
		font-family: 'DotGothic16', sans-serif;
	}
</style>