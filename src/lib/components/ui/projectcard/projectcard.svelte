<script lang="ts">
	import { Motion, useMotionTemplate, useMotionValue } from 'svelte-motion';
	import Projectdialog from '$lib/components/ui/projectdialog/projectdialog.svelte';
	import Proximityglow from '$lib/components/ui/proximityglow/proximityglow.svelte';

	export let title;
	export let overview;
	export let videoPath;
	export let keyFeatures;
	export let thumbnail;
	export let note;
	export let isSpecial;
	export let noteColor;
	export let date;

	let cardElement: HTMLDivElement;
	let mouseX = useMotionValue(0);
	let mouseY = useMotionValue(0);
	let rotationX = 0;
	let rotationY = 0;
	let scale = 1;
	let shadowX = 0;
	let shadowY = 0;

	let background = useMotionTemplate`radial-gradient(200px circle at ${mouseX}px ${mouseY}px, rgba(51, 51, 51, 0.4), transparent 80%)`;

	function handleMouseMove(event: { clientX: number; clientY: number }) {
		if (window.innerWidth > 768) {
			const rect = cardElement.getBoundingClientRect();
			const cardWidth = rect.width;
			const cardHeight = rect.height;
			const centerX = rect.left + cardWidth / 2;
			const centerY = rect.top + cardHeight / 2;
			const mouseXVal = event.clientX - centerX;
			const mouseYVal = event.clientY - centerY;

			const maxRotation = 10;
			rotationY = (mouseXVal / (cardWidth / 2)) * maxRotation;
			rotationX = -(mouseYVal / (cardHeight / 2)) * maxRotation;
			scale = 1.02;

			const maxShadow = 30;
			shadowX = (mouseXVal / (cardWidth / 2)) * maxShadow;
			shadowY = (mouseYVal / (cardHeight / 2)) * maxShadow;

			mouseX.set(event.clientX - rect.left);
			mouseY.set(event.clientY - rect.top);
		}
	}

	function handleMouseLeave() {
		rotationX = 0;
		rotationY = 0;
		scale = 1;
		shadowX = 0;
		shadowY = 0;
	}
</script>

<Proximityglow>
	<div
		class="card group relative h-[360px] max-w-[350px] overflow-hidden rounded-xl bg-neutral-950 sm:h-[500px] md:h-[500px] lg:h-[500px]"
		bind:this={cardElement}
		on:mousemove={handleMouseMove}
		on:mouseleave={handleMouseLeave}
		role="group"
		style="transform: perspective(800px) rotateX({rotationX}deg) rotateY({rotationY}deg) scale({scale});
			 transition: transform 0.2s ease-out, box-shadow 0.2s ease-out;
			 box-shadow: {shadowX}px {shadowY}px 50px rgba(0, 0, 0, 0.2);"
	>
		<div
			class="absolute right-5 top-0 h-px w-80 bg-gradient-to-l from-transparent via-white/30 via-10% to-transparent"
		/>
		<Motion
			style={{
				background
			}}
			let:motion
		>
			<div
				use:motion
				class="pointer-events-none absolute -inset-px rounded-xl opacity-0 transition duration-300 group-hover:opacity-100"
			></div>
		</Motion>
		<div class="relative flex h-full flex-col gap-3 rounded-xl border border-white/10 px-4 py-5">
			<div class="flex-grow space-y-2">
				<img
					src={thumbnail}
					alt="Project Thumbnail"
					class="h-36 w-full rounded-xl object-cover opacity-75 sm:h-52 md:h-52 lg:h-52"
				/>
				<div class="flex flex-row items-center justify-between pt-2">
					<h3 class="text-[15px] font-semibold text-neutral-200 sm:text-xl">{title}</h3>
					<p class="select-none text-[9px] text-neutral-300 sm:text-[13px]">{date}</p>
				</div>
				<p class="line-clamp-3 pb-3 text-[11px] leading-[1.5] text-neutral-400 sm:text-sm">
					{overview.length > 100 ? `${overview.slice(0, 100)}...` : overview}
				</p>
			</div>
			<div class="button">
				<Projectdialog
					{title}
					{overview}
					{videoPath}
					{keyFeatures}
					{note}
					{isSpecial}
					{noteColor}
				/>
			</div>
		</div>
	</div>
</Proximityglow>

<style>
	.card {
		border-radius: 16px;
		margin: 16px;
		border: 2px solid transparent;
		transition:
			transform 0.1s ease-out,
			box-shadow 0.2s ease-out,
			border 0.3s ease-out;
		overflow: hidden;
		background: #1e1e1e;
		display: flex;
		flex-direction: column;
		align-items: center;
		position: relative;
	}

	.card:hover {
		border-image: linear-gradient(45deg, #ff0266, #ff5959) 1;
	}

	.button button {
		background-color: #ff0266;
		color: #ffffff;
		border: none;
		padding: 10px 20px;
		border-radius: 8px;
		cursor: pointer;
		transition:
			background-color 0.2s,
			transform 0.2s;
	}

	.button button:hover {
		background-color: #e6005c;
		transform: translateY(-2px);
	}

	.card::before {
		content: '';
		position: absolute;
		top: -50%;
		left: -50%;
		width: 200%;
		height: 200%;
		background: radial-gradient(circle, rgba(255, 2, 102, 0.15), transparent 70%);
		transform: scale(0);
		transition: transform 0.5s ease-out;
		z-index: -1;
	}

	.card:hover::before {
		transform: scale(1);
	}

	.line-clamp-3 {
		display: -webkit-box;
		-webkit-line-clamp: 3;
		-webkit-box-orient: vertical;
		overflow: hidden;
	}

	@media (min-width: 768px) {
		.card {
			margin: 16px;
		}
	}
</style>
