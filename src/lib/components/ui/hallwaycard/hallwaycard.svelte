<script lang="ts">
	// Variables for tilt and scale effects
	let cardElement: HTMLDivElement;
	let rotationX = 0;
	let rotationY = 0;
	let scale = 1;
	let shadowX = 0;
	let shadowY = 0;
	let animationFrameId: number;

	export let ImagePath = '';
	export let BackImagePath = '';
	export let maxRotation = 10; // Maximum rotation in degrees
	export let maxShadow = 30; // Maximum shadow offset
	export let IsStar = true; // Enable or disable sparkles layer
	export let IsGradient = true; // Enable or disable gradient layer
	export let StarStrength = 0.4; // Opacity of the sparkles layer
	export let GradientStrength = 0.4; // Opacity of the gradient layer

	function handleMouseMove(event: { clientX: number; clientY: number }) {
		if (animationFrameId) {
			cancelAnimationFrame(animationFrameId);
		}
		animationFrameId = requestAnimationFrame(() => {
			const rect = cardElement.getBoundingClientRect();
			const cardWidth = rect.width;
			const cardHeight = rect.height;
			const centerX = rect.left + cardWidth / 2;
			const centerY = rect.top + cardHeight / 2;
			const mouseX = event.clientX - centerX;
			const mouseY = event.clientY - centerY;

			rotationY = (mouseX / (cardWidth / 2)) * maxRotation;
			rotationX = -(mouseY / (cardHeight / 2)) * maxRotation;

			// Scale effect
			scale = 1.05;

			// Shadow effect
			shadowX = (mouseX / (cardWidth / 2)) * maxShadow;
			shadowY = (mouseY / (cardHeight / 2)) * maxShadow;

			// Update gradient and sparkles position
			const gradientLayer = cardElement.querySelector('.gradient-layer') as HTMLDivElement;
			const sparklesLayer = cardElement.querySelector('.sparkles-layer') as HTMLDivElement;
			if (gradientLayer && sparklesLayer) {
				gradientLayer.style.backgroundPosition = `${50 + (mouseX / cardWidth) * 100}% ${50 + (mouseY / cardHeight) * 100}%`;
				sparklesLayer.style.backgroundPosition = `${50 + (mouseX / cardWidth) * 50}% ${50 + (mouseY / cardHeight) * 50}%`;
			}
		});
	}

	function handleMouseLeave() {
		if (animationFrameId) {
			cancelAnimationFrame(animationFrameId);
		}
		rotationX = 0;
		rotationY = 0;
		scale = 1;
		shadowX = 0;
		shadowY = 0;
	}
</script>

<div
	class="card"
	bind:this={cardElement}
	on:mousemove={handleMouseMove}
	on:mouseleave={handleMouseLeave}
	style="
      transform: perspective(800px) rotateX({rotationX}deg) rotateY({rotationY}deg) scale({scale});
      transition: transform 0.1s linear, box-shadow 0.2s ease;
      box-shadow: {-shadowX}px {shadowY}px 50px rgba(0, 0, 0, 0.2);
    "
>
	<img src={ImagePath} alt="Card Image" class="card-image" />
	{#if IsGradient}
		<div class="gradient-layer" style="opacity: {GradientStrength};"></div>
	{/if}
	{#if IsStar}
		<div class="sparkles-layer" style="opacity: {StarStrength};"></div>
	{/if}
</div>

<style>
	:root {
		--color1: rgb(0, 231, 255);
		--color2: rgb(255, 0, 231);
	}

	.card {
		aspect-ratio: 5 / 7;
		border-radius: 16px;
		margin: 16px;
		overflow: hidden;
		position: relative;
		background: #040712;
		transition:
			transform 0.5s ease,
			box-shadow 0.2s ease;
		display: flex;
		align-items: center;
		justify-content: center;
		width: 100%;
		max-width: 400px;
		box-shadow:
			0 0 20px -5px var(--color1),
			0 0 20px -5px var(--color2),
			0 0 50px rgba(0, 0, 0, 0.5);
		will-change: transform, filter;
	}

	.card:hover {
		box-shadow:
			0 0 30px -5px var(--color1),
			0 0 30px -5px var(--color2),
			0 0 50px rgba(0, 0, 0, 0.5);
	}

	.gradient-layer {
		position: absolute;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		background-image: linear-gradient(
			115deg,
			transparent 0%,
			var(--color1) 25%,
			transparent 50%,
			var(--color2) 75%,
			transparent 100%
		);
		background-size: 200% 200%;
		mix-blend-mode: color-dodge;
		pointer-events: none;
		transition: all 0.33s ease;
		z-index: 2;
	}

	.sparkles-layer {
		position: absolute;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		background-image: url('https://assets.codepen.io/13471/sparkles.gif'),
			linear-gradient(
				125deg,
				#ff008450 15%,
				#fca40040 30%,
				#ffff0030 40%,
				#00ff8a20 60%,
				#00cfff40 70%,
				#cc4cfa50 85%
			);
		background-size: 150%;
		background-blend-mode: overlay;
		mix-blend-mode: color-dodge;
		pointer-events: none;
		transition: all 0.33s ease;
		z-index: 3;
	}

	.card-image {
		width: 100%;
		height: 100%;
		object-fit: cover;
		z-index: 1;
	}
</style>
