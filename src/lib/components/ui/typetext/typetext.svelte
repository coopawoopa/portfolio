<script>
	import { onMount, onDestroy } from 'svelte';
	import { slide } from 'svelte/transition';
	import GradualSpacing from '$lib/components/ui/GradualSpacing/GradualSpacing.svelte';

	let greetings = ['Hello', 'Welcome!', 'Fedor Agafonov'];
	let index = 0;
	let roller;
	let showGradualSpacing = false;

	onMount(() => {
		roller = setInterval(() => {
			if (index === greetings.length - 1) {
				index = greetings.length - 1;
				clearInterval(roller);
				showGradualSpacing = true; // Show the GradualSpacing component once the roller finishes
			} else {
				index++;
			}
		}, 1250);
	});

	onDestroy(() => {
		clearInterval(roller);
	});
</script>

<div class="relative inline-block">
	<div class="inline-block align-middle">
		{#key index}
			<h1 class=" text-4xl font-bold" transition:slide>
				{greetings[index]}
			</h1>
		{/key}
	</div>

	{#if showGradualSpacing}
		<div class="absolute right-0">
			<GradualSpacing
				class="font-display align-middle font-bold tracking-[-0.01em] text-black dark:text-white"
				words="Portfolio"
			/>
		</div>
	{/if}
</div>
