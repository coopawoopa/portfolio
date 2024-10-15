<script>
	import { onMount, onDestroy } from 'svelte';
	import { slide } from 'svelte/transition';

	let greetings = ['Hello', 'Welcome!', 'Fedor Agafonov'];
	let index = 0;
	let roller;

	onMount(() => {
		roller = setInterval(() => {
			if (index === greetings.length - 1) index = greetings.length - 1;
			else index++;
		}, 1250);
	});

	onDestroy(() => {
		clearInterval(roller);
	});
</script>

{#key index}
	<h1 class="text-4xl font-bold pb-4" transition:slide>{greetings[index]}</h1>
{/key}