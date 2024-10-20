<script lang="ts">
	import { cn } from '$lib/utils';
	import { AnimatePresence, Motion } from 'svelte-motion';

	let className: any = 'Portfolio';
	export { className as class };

	export let words = 'Portfolio';
	export let duration = 0.2;
	export let delayMultiple = 0.01;
	export let framerProps = {
		hidden: { opacity: 0, x: -20 },
		visible: { opacity: 1, x: 0 }
	};
	let wordssplit = words.split('');
</script>

<div class="flex justify-center space-x-1">
	<AnimatePresence let:item list={[{ key: wordssplit }]}>
		{#each wordssplit as char, i}
			<Motion
				initial="hidden"
				animate="visible"
				exit="hidden"
				variants={framerProps}
				transition={{
					duration: duration,
					delay: i * delayMultiple
				}}
				let:motion
			>
				<span use:motion class={cn('gradient-text drop-shadow-sm', className)}>
					{#if char === ' '}
						<span>&nbsp;</span>
					{:else}
						{char}
					{/if}
				</span>
			</Motion>
		{/each}
	</AnimatePresence>
</div>

<style>
	@keyframes gradient {
		0% {
			background: linear-gradient(90deg, #ff7e5f, #feb47b);
			-webkit-background-clip: text;
			color: transparent;
		}
		100% {
			color: white;
		}
	}

	.gradient-text {
		animation: gradient 1s ease forwards;
	}
</style>
