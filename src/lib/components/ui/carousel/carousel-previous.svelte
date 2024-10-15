<script lang="ts">
	import ArrowLeft from 'lucide-svelte/icons/arrow-left';
	import type { VariantProps } from 'tailwind-variants';
	import { getEmblaContext } from './context.js';
	import { cn } from '$lib/utils.js';
	import { Button, type Props, type buttonVariants } from '$lib/components/ui/button/index.js';

	type $$Props = Props;

	let className: $$Props['class'] = undefined;
	export { className as class };
	export let variant: VariantProps<typeof buttonVariants>['variant'] = 'ghost';
	export let size: VariantProps<typeof buttonVariants>['size'] = 'icon';

	const { orientation, canScrollPrev, scrollPrev, handleKeyDown } =
		getEmblaContext('<Carousel.Previous/>');

	// State for hover effect
	let isHovered = false;
</script>

<Button
	{variant}
	{size}
	class={cn(
		'absolute h-16 w-16 items-center justify-center rounded-full',
		'bg-[rgba(30,30,30,0.2)] text-white backdrop-blur-sm',
		'transform transition duration-100 ease-in-out',
		$orientation === 'horizontal'
			? 'top-100 -left-0 m-2 rounded-md px-4'
			: 'left-1/2 top-4 -translate-x-1/2 rotate-90',
		'hover:scale-105 hover:bg-[rgba(255,2,102,0.9)]',
		className
	)}
	disabled={!$canScrollPrev}
	on:click={scrollPrev}
	on:keydown={handleKeyDown}
	on:mouseenter={() => (isHovered = true)}
	on:mouseleave={() => (isHovered = false)}
	aria-label="Previous slide"
>
	<ArrowLeft class="h-6 w-6 transition-transform duration-300 ease-in-out" />
</Button>
