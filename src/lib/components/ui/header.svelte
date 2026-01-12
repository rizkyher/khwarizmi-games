<script lang="ts">
	// Definisikan tipe props agar tidak terjadi error 'never'
	interface Props {
		title: string;
		subtitle: string;
	}

	// Svelte 5 menggunakan $props() untuk menerima data dari parent
	let { title, subtitle }: Props = $props();
</script>

<header class="text-center mb-16 mt-10">
	<div class="inline-block relative">
		<h1 class="text-5xl md:text-7xl font-bold text-slate-800 mb-4 tracking-tight uppercase italic">
			{title}
		</h1>
		<div class="h-2 w-full bg-blue-400 border-2 border-black absolute -bottom-2 shadow-[4px_4px_0_0_#000]"></div>
	</div>
	<p class="mt-8 text-slate-600 text-lg font-medium">{subtitle}</p>
</header>