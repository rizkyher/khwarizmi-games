<script lang="ts">
	// Kita buat beberapa data awan dengan posisi dan kecepatan berbeda
	// agar tercipta efek kedalaman (parallax)
	const cloudLayers = [
		{ top: '10%', duration: '35s', scale: '0.8', opacity: '0.4', delay: '0s' },
		{ top: '25%', duration: '25s', scale: '1.2', opacity: '0.6', delay: '-5s' },
		{ top: '45%', duration: '45s', scale: '1.0', opacity: '0.3', delay: '-10s' },
		{ top: '70%', duration: '30s', scale: '1.5', opacity: '0.5', delay: '-15s' },
		{ top: '85%', duration: '55s', scale: '0.7', opacity: '0.4', delay: '-20s' }
	];
</script>

<div class="fixed inset-0 pointer-events-none overflow-hidden z-[-1]">
	{#each cloudLayers as cloud}
		<div 
			class="absolute left-[-300px] animate-drift"
			style="
				top: {cloud.top}; 
				animation-duration: {cloud.duration}; 
				animation-delay: {cloud.delay};
				transform: scale({cloud.scale});
				opacity: {cloud.opacity};
			"
		>
			<div class="relative w-32 h-12 bg-white shadow-[8px_8px_0_0_rgba(0,0,0,0.05)]">
				<div class="absolute -top-6 left-6 w-12 h-12 bg-white"></div>
				<div class="absolute -top-4 left-16 w-16 h-10 bg-white"></div>
				<div class="absolute bottom-0 left-0 w-full h-2 bg-slate-200/50"></div>
			</div>
		</div>
	{/each}
</div>

<style>
	/* Animasi untuk menggerakkan awan dari kiri ke kanan layar */
	@keyframes drift {
		from {
			transform: translateX(-20vw) scale(var(--tw-scale-x));
		}
		to {
			transform: translateX(120vw) scale(var(--tw-scale-x));
		}
	}

	.animate-drift {
		animation: drift linear infinite;
		will-change: transform;
	}
</style>