<script lang="ts">
	import ArrowRight from 'lucide-svelte/icons/arrow-right';
	import type { VariantProps } from 'tailwind-variants';
	import { getEmblaContext } from './context.js';
	import { cn } from '$lib/utils.js';
	import { Button, type Props, type buttonVariants } from '$lib/components/ui/button/index.js';

	type $$Props = Props;

	let className: $$Props['class'] = undefined;
	export { className as class };
	export let variant: VariantProps<typeof buttonVariants>['variant'] = 'ghost';
	export let size: VariantProps<typeof buttonVariants>['size'] = 'icon';
	const { orientation, canScrollNext, scrollNext, handleKeyDown } =
		getEmblaContext('<Carousel.Next/>');
</script>

<Button
	{variant}
	{size}
	class={cn(
		'absolute h-16 w-16 items-center justify-center rounded-full',
		'bg-[rgba(30,30,30,0.2)] text-white backdrop-blur-sm',
		'transform transition duration-100 ease-in-out',

		$orientation === 'horizontal'
			? 'top-100 left-20 m-2 rounded-md px-4'
			: '-bottom-12 left-1/2 -translate-x-1/2 rotate-90',
		'hover:scale-105 hover:bg-[rgba(255,2,102,0.9)]',
		className
	)}
	disabled={!$canScrollNext}
	on:click={scrollNext}
	on:keydown={handleKeyDown}
	{...$$restProps}
>
	<ArrowRight class="h-6 w-6 transition-transform duration-300 ease-in-out" />
</Button>
