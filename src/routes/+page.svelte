<script lang="ts">
	// Import semua komponen yang telah dibuat
	import Navbar from '$lib/components/ui/Navbar.svelte';
	import Clouds from '$lib/components/ui/Clouds.svelte';
	import Header from '$lib/components/ui/Header.svelte';
	import GameCard from'$lib/components/ui/GameCard.svelte';
	import Footer from '$lib/components/ui/Footer.svelte';

	// Data Game - Menggunakan Svelte 5 $state jika nantinya ingin difilter
	let myGames = $state([
		{ 
			id: 1, 
			title: "Cyber Drift", 
			desc: "Hindari rintangan di dunia neon masa depan dengan kecepatan tinggi.", 
			tags: ["Action", "Sci-Fi"], 
			color: "bg-cyan-400" 
		},
		{ 
			id: 2, 
			title: "Spirit Woods", 
			desc: "Petualangan puzzle santai di dalam hutan yang penuh dengan roh baik.", 
			tags: ["Cozy", "Puzzle"], 
			color: "bg-emerald-400" 
		},
		{ 
			id: 3, 
			title: "Sky Castle", 
			desc: "Bangun kerajaanmu di atas awan dan lindungi dari serangan naga.", 
			tags: ["Strategy", "Fantasy"], 
			color: "bg-sky-300" 
		},
		{ 
			id: 4, 
			title: "Totoro Run", 
			desc: "Lari secepat mungkin untuk mengejar Bus Kucing sebelum hujan turun.", 
			tags: ["Runner", "Ghibli"], 
			color: "bg-orange-300" 
		},
		{ 
			id: 5, 
			title: "Pixel Chef", 
			desc: "Masak makanan lezat untuk para petualang yang mampir ke kedaimu.", 
			tags: ["Simulation"], 
			color: "bg-rose-400" 
		},
		{ 
			id: 6, 
			title: "Star Gazing", 
			desc: "Hubungkan rasi bintang untuk mengungkap cerita kuno di langit malam.", 
			tags: ["Educational"], 
			color: "bg-indigo-400" 
		}
	]);
</script>

<Clouds />

<Navbar />

<main class="relative z-10 min-h-screen">
	<div class="max-w-6xl mx-auto px-6 py-12">
		
		<section id="home">
			<Header 
				title="PIXEL GHIBLI" 
				subtitle="Koleksi petualangan kecil dalam balutan pixel art dan estetika Ghibli." 
			/>
		</section>

		<div class="my-16 flex justify-center items-center gap-4">
			<div class="h-1 flex-grow bg-black shadow-[0_2px_0_0_#fff]"></div>
			<div class="w-4 h-4 bg-yellow-400 border-2 border-black rotate-45"></div>
			<div class="h-1 flex-grow bg-black shadow-[0_2px_0_0_#fff]"></div>
		</div>

		<section id="games" class="scroll-mt-32">
			<div class="flex justify-between items-end mb-10">
				<h2 class="text-3xl font-black text-slate-800 uppercase italic">
					Featured <span class="text-blue-600">Games</span>
				</h2>
				<p class="text-sm font-bold text-slate-500 hidden md:block uppercase tracking-widest">
					Total: {myGames.length} Projects
				</p>
			</div>

			<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-10 lg:gap-14">
				{#each myGames as game (game.id)}
					<GameCard {game} />
				{/each}
			</div>
		</section>

	</div>

	<Footer creator="NamaKamu" />
</main>

<style>
	/* Import Font Utama di App.svelte agar tersedia global */
	@import url('https://fonts.googleapis.com/css2?family=DotGothic16&display=swap');

	:global(html) {
		scroll-behavior: smooth;
	}

	:global(body) {
		margin: 0;
		padding: 0;
		font-family: 'DotGothic16', sans-serif;
		/* Gradasi Langit Ghibli */
		background: linear-gradient(to bottom, #bae6fd 0%, #e0f2fe 50%, #f0f9ff 100%);
		color: #1e293b;
		overflow-x: hidden;
	}

	/* Gaya khusus untuk scrollbar agar terlihat retro */
	:global(::-webkit-scrollbar) {
		width: 12px;
	}
	:global(::-webkit-scrollbar-track) {
		background: #000;
	}
	:global(::-webkit-scrollbar-thumb) {
		background: #fbbf24;
		border: 3px solid #000;
	}
</style>