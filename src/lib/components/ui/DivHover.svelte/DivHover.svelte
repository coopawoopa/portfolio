<script lang="ts">
	import { spring } from 'svelte/motion';
	import { fade } from 'svelte/transition';

	let width = spring(120);
	let height = spring(30);
	let rounded = spring(50);
	let isChanged = false;
	let bwidth = spring(1);
	let opacity = spring(1);

	let animationElement = (node: HTMLElement) => {
		let changeSize = () => {
			width.set(230);
			height.set(145);
			rounded.set(20);
			opacity.set(1);
			isChanged = true;
		};
		let originalSize = () => {
			width.set(120);
			height.set(30);
			rounded.set(50);
			bwidth.set(1);
			opacity.set(1);
			isChanged = false;
		};

		node.addEventListener('mouseenter', changeSize);
		node.addEventListener('mouseleave', originalSize);
		return {
			destroy() {
				node.removeEventListener('mouseenter', changeSize);
				node.removeEventListener('mouseleave', originalSize);
			}
		};
	};
	let avatars = [
		{
			src: 'https://i.pinimg.com/564x/ea/8b/06/ea8b06307f2f6f0a6f6041d3f492d013.jpg',
			alt: 'bhide',
			fallback: 'SM',
			name: 'Saloni'
		}
	];
</script>

<div class="flex items-center justify-center">
	<div
		id="animationElement"
		use:animationElement
		class="flex flex-col items-center justify-center rounded-lg"
		style="width: {$width}px; height:{$height}px; border-radius: {$rounded}px; border-width: {$bwidth}px; opacity: {$opacity}"
	>
		{#if isChanged}
			<div class="relative w-full p-2.5">
				<div in:fade={{ duration: 600 }}>
					{#each avatars as { src, alt, fallback, name }}
						<div
							class="m-1 flex items-center justify-between gap-3 rounded-full border border-primary p-1 hover:bg-primary/10"
						>
							<h4 class="m-auto font-mono">{'a.f.1352@mail.ru'}</h4>
						</div>
						<div
							class="m-1 flex items-center justify-between gap-3 rounded-full border border-primary p-1 hover:bg-primary/10"
						>
							<h4 class="m-auto font-mono">
								<a href="https://www.linkedin.com/in/fedor-agafonov-93579b230/" target="_blank"
									>LinkedIn</a
								>
							</h4>
						</div>
						<div
							class="m-1 flex items-center justify-between gap-3 rounded-full border border-primary p-1 hover:bg-primary/10"
						>
							<h4 class="m-auto font-mono">
								<a href="https://github.com/coopawoopa" target="_blank">GitHub</a>
							</h4>
						</div>
					{/each}
				</div>
			</div>
		{:else}
			<div
				in:fade={{
					duration: 500,
					delay: 200
				}}
				class="flex h-full items-center justify-center"
			>
				Contact Me
			</div>
		{/if}
	</div>
</div>
