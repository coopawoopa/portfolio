<script lang="ts">
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

	// Variables for tilt and scale effects
	let cardElement: HTMLDivElement;
	let rotationX = 0;
	let rotationY = 0;
	let scale = 1;
	let shadowX = 0;
	let shadowY = 0;

	function handleMouseMove(event: { clientX: number; clientY: number }) {
		const rect = cardElement.getBoundingClientRect();
		const cardWidth = rect.width;
		const cardHeight = rect.height;
		const centerX = rect.left + cardWidth / 2;
		const centerY = rect.top + cardHeight / 2;
		const mouseX = event.clientX - centerX;
		const mouseY = event.clientY - centerY;

		const maxRotation = 10; // Maximum rotation in degrees
		rotationY = (mouseX / (cardWidth / 2)) * maxRotation;
		rotationX = -(mouseY / (cardHeight / 2)) * maxRotation;

		// Scale effect
		scale = 1.02;

		// Shadow effect
		const maxShadow = 30; // Maximum shadow offset
		shadowX = (mouseX / (cardWidth / 2)) * maxShadow;
		shadowY = (mouseY / (cardHeight / 2)) * maxShadow;
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
		class="card"
		bind:this={cardElement}
		on:mousemove={handleMouseMove}
		on:mouseleave={handleMouseLeave}
		style="
			transform: perspective(800px) rotateX({rotationX}deg) rotateY({rotationY}deg) scale({scale});
			transition: transform 0.2s ease-out, box-shadow 0.2s ease-out;
			box-shadow: {-shadowX}px {shadowY}px 50px rgba(0, 0, 0, 0.2);
		"
	>
		<div class="header">
			<h3
				class="flex h-full scroll-m-20 items-center justify-center text-2xl font-semibold tracking-tight"
			>
				{title}
			</h3>
		</div>
		<img src={thumbnail} alt="Project Thumbnail" class="thumbnail" />
		<div class="button">
			<Projectdialog {title} {overview} {videoPath} {keyFeatures} {note} {isSpecial} {noteColor} />
		</div>
	</div>
</Proximityglow>

<style>
	.card {
		min-height: 300px;
		border-radius: 16px;
		margin: 16px;
		border: 2px solid transparent;
		transition:
			transform 0.1s ease-out,
			box-shadow 0.2s ease-out,
			border 0.3s ease-out;
		align-items: center;
		justify-content: center;
		flex-direction: column;
		display: flex;
		position: relative;
		overflow: hidden;
		background: #1e1e1e;
	}

	.card:hover {
		border-image: linear-gradient(45deg, #ff0266, #ff5959) 1;
	}

	.header {
		width: 100%;
		height: 100px;
		background: linear-gradient(-45deg, #000000, #040303, #0f1315, #111716);
		background-size: 400% 400%;
		animation: gradient 15s ease infinite;
		padding: 20px;
		border-top-left-radius: 16px;
		border-top-right-radius: 16px;
		text-align: center;
		font-size: 1.5rem;
		color: #ffffff;
	}

	@keyframes gradient {
		0% {
			background-position: 0% 50%;
		}
		50% {
			background-position: 100% 50%;
		}
		100% {
			background-position: 0% 50%;
		}
	}

	.thumbnail {
		width: 100%;
		height: 200px;
		object-fit: cover;
		transition: transform 0.2s ease-out;
	}

	.card:hover .thumbnail {
		transform: scale(1.02);
	}

	.button {
		position: absolute;
		bottom: 20px;
		right: 20px;
		z-index: 100;
	}

	/* Add a subtle glow effect on hover */
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

	/* Optional: Add interactive tilt to the button */
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

	/* Responsive adjustments */
	@media (max-width: 768px) {
		.card {
			min-height: 250px;
		}

		.header {
			height: 80px;
		}

		.thumbnail {
			height: 150px;
		}
	}
</style>
