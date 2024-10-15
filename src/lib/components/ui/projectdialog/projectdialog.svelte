<script lang="ts">
	import * as Dialog from '$lib/components/ui/dialog';
	import * as Drawer from '$lib/components/ui/drawer/index.js';
	import { ScrollArea } from '$lib/components/ui/scroll-area/index.js';
	import { Button, buttonVariants } from '$lib/components/ui/button/index.js';
	import { mediaQuery } from 'svelte-legos';
	import Hallwaycard from '../hallwaycard/hallwaycard.svelte';
	import { Skeleton } from '$lib/components/ui/skeleton';

	export let title = 'Product Details';
	export let overview = 'This is the overview of the product';
	export let videoPath = '';
	export let note = '';
	export let isSpecial = 'no';
	export let noteColor = '';

	interface KeyFeature {
		title: string;
		description: string;
		gifPaths: string[];
		orientation: 'gif-desc' | 'desc-gif' | 'gif-desc-row';
	}

	function createKeyFeature(
		title: string,
		description: string,
		gifPaths: string[],
		orientation: 'gif-desc' | 'desc-gif' | 'gif-desc-row'
	): KeyFeature {
		return { title, description, gifPaths, orientation };
	}

	export let keyFeatures = [
		createKeyFeature('Feature 1', 'Description 1', ['/path/to/gif1', '/path/to/gif2'], 'gif-desc'),
		createKeyFeature('Feature 2', 'Description 2', ['/path/to/gif3'], 'desc-gif'),
		createKeyFeature(
			'Feature 3',
			'Description 3',
			['/path/to/gif4', '/path/to/gif5', '/path/to/gif6'],
			'gif-desc-row'
		)
	];

	let open = false;
	const isDesktop = mediaQuery('(min-width: 768px)'); // Media query to detect screen size
	let dialogContent: HTMLElement | null;

	import { onMount } from 'svelte';

	onMount(() => {
		if (dialogContent) {
			dialogContent.scrollTop = 0;
		}
	});

	let imageLoadedStates = keyFeatures.map((feature) => feature.gifPaths.map(() => false));
</script>

{#if $isDesktop}
	<!-- Dialog for Desktop -->
	<Dialog.Root bind:open>
		<Dialog.Trigger class={buttonVariants({ variant: 'outline', size: 'lg' })}>
			See Project
		</Dialog.Trigger>
		<Dialog.Content class="sm:max-w-[80%]">
			<!-- svelte-ignore a11y-autofocus -->
			<input class="fixed left-0 top-0 h-0 w-0" type="checkbox" autofocus={true} />
			<div class="dialog-content" bind:this={dialogContent}>
				<!-- Dialog content goes here -->
				<div class="container">
					<h1 class="scroll-m-20 text-4xl font-extrabold tracking-tight lg:text-5xl">{title}</h1>
					<!-- Overview and other details -->
					<div class="card">
						<div class="overview">
							<ScrollArea class="h-full w-full rounded-md">
								<div class="p-4">
									<h4 class="text-lg font-semibold">Overview</h4>
									<p class="font-normal leading-7 text-gray-300">{overview}</p>
								</div>
							</ScrollArea>
						</div>
						{#if note !== ''}
							<div class="special" style={`background: ${noteColor}`}>
								<p>{note}</p>
							</div>
						{/if}
						{#if isSpecial === 'yes'}
							<div style="display: flex; gap: 20px; margin: 20px;">
								<Hallwaycard
									ImagePath="https://i.postimg.cc/q7cfTgdP/Lester-4x.png"
									GradientStrength={0.2}
								/>
								<Hallwaycard
									ImagePath="https://i.postimg.cc/QtbrpC4Q/Tomohide-Tseki-Plus-4x.png"
									GradientStrength={0.2}
								/>
								<Hallwaycard
									ImagePath="https://i.postimg.cc/3xv5tnfJ/Galka-World-Eater-4x.png"
									GradientStrength={0.1}
								/>
							</div>
							<div class="key-feature">
								<ScrollArea class="h-full w-full rounded-md border">
									<div class="p-4">
										<h4 class="scroll-m-20 text-xl font-bold tracking-tight">
											{'Holo/Foil Cards'}
										</h4>
										<p class="font-normal leading-7 text-gray-300">
											{'Just like MTG and Pokemon, or any other trading card game, cards would ahve rarities, however, said rarity will only determine the status and style of card in play, power level itself is entirely independent. This also means no one card is tied to another. Making a deck would be like brewing a potion.'}
										</p>
									</div>
								</ScrollArea>
							</div>
							<div style="display: flex; gap: 20px; margin: 20px;">
								<Hallwaycard
									ImagePath="https://i.postimg.cc/hGVntpV3/AReally-Big-Rock-4x.png"
									IsStar={false}
									IsGradient={false}
								/>
								<Hallwaycard
									ImagePath="https://i.postimg.cc/Y0DKsVwj/Bob-The-Giant-4x.png"
									IsStar={false}
									IsGradient={false}
								/>
								<Hallwaycard
									ImagePath="https://i.postimg.cc/Bnrs3dPK/Toska-4x.png"
									IsStar={false}
									IsGradient={false}
								/>
							</div>
							<ScrollArea class="h-full w-full rounded-md border">
								<div class="p-4">
									<h4 class="scroll-m-20 text-xl font-bold tracking-tight">
										{'Small portion'}
									</h4>
									<p class="font-normal leading-7 text-gray-300">
										{'This game is not fully complete and new rules and cards are figured out every day. The game is focused on being competeive and fair no matter how rich you are. These are only a small portion of both complete and incomplete cards.'}
									</p>
								</div>
							</ScrollArea>
							<div style="display: flex; gap: 20px; margin: 20px;">
								<Hallwaycard
									ImagePath="https://i.postimg.cc/5tWcTLD5/Justin-4x.png"
									IsStar={false}
									IsGradient={false}
								/>
								<Hallwaycard
									ImagePath="https://i.postimg.cc/Fs1QL9jS/Dacada-4x.png"
									IsStar={false}
									IsGradient={false}
								/>
								<Hallwaycard
									ImagePath="https://i.postimg.cc/wvHpyLVx/Pugh-4x.png"
									IsStar={false}
									IsGradient={false}
								/>
							</div>
							<ScrollArea class="h-full w-full rounded-md border">
								<div class="p-4">
									<h4 class="scroll-m-20 text-xl font-bold tracking-tight">
										{'Dynamic Gameplay'}
									</h4>
									<p class="font-normal leading-7 text-gray-300">
										{'There are features to this game that I like to call dynamic. They spice the game up without having the user do anything, this howwever does not mean that the user has no influence on said effects. For example Sanity and Rage similar to that of Darkest Dungeon.'}
									</p>
								</div>
							</ScrollArea>
							<div style="display: flex; gap: 20px; margin: 20px;">
								<Hallwaycard
									ImagePath="https://i.postimg.cc/zDxrvLR5/Dniprokovie-4x.png"
									IsStar={false}
									IsGradient={false}
								/>
								<Hallwaycard
									ImagePath="https://i.postimg.cc/HsK10f2h/Finn-4x.png"
									IsStar={false}
									IsGradient={false}
								/>
								<Hallwaycard
									ImagePath="https://i.postimg.cc/fyRQ5sp6/Backside-4x.png"
									IsStar={false}
									IsGradient={false}
								/>
							</div>
						{/if}
						<!-- Features -->
						{#each keyFeatures as keyFeature, featureIndex}
							{#if keyFeature.gifPaths.length !== 0}
								<div class={`features-and-gifs ${keyFeature.orientation}`}>
									{#if keyFeature.gifPaths.length === 1}
										{#if keyFeature.orientation === 'gif-desc'}
											<div class="gif">
												{#if !imageLoadedStates[featureIndex][0]}
													<Skeleton class="h-[300px] w-[500px] rounded-md" />
												{/if}
												<img
													src={keyFeature.gifPaths[0]}
													alt="GIF"
													on:load={() => {
														imageLoadedStates[featureIndex][0] = true;
													}}
													style:display={!imageLoadedStates[featureIndex][0] ? 'none' : 'block'}
												/>
											</div>
											<div class="key-feature">
												<ScrollArea class="h-full w-full rounded-md border">
													<div class="p-4">
														<h4 class="scroll-m-20 text-xl font-bold tracking-tight">
															{keyFeature.title}
														</h4>
														<p class="font-normal leading-7 text-gray-300">
															{keyFeature.description}
														</p>
													</div>
												</ScrollArea>
											</div>
										{:else if keyFeature.orientation === 'desc-gif'}
											<div class="key-feature">
												<ScrollArea class="h-full w-full rounded-md border">
													<div class="p-4">
														<h4 class="scroll-m-20 text-xl font-bold tracking-tight">
															{keyFeature.title}
														</h4>
														<p class="font-normal leading-7 text-gray-300">
															{keyFeature.description}
														</p>
													</div>
												</ScrollArea>
											</div>
											<div class="gif">
												{#if !imageLoadedStates[featureIndex][0]}
													<Skeleton class="h-[300px] w-[500px] rounded-md" />
												{/if}
												<img
													src={keyFeature.gifPaths[0]}
													alt="GIF"
													on:load={() => {
														imageLoadedStates[featureIndex][0] = true;
													}}
													style:display={!imageLoadedStates[featureIndex][0] ? 'none' : 'block'}
												/>
											</div>
										{:else if keyFeature.orientation === 'gif-desc-row'}
											<div class="gif-row">
												{#if !imageLoadedStates[featureIndex][0]}
													<Skeleton class="h-[300px] w-[500px] rounded-md" />
												{/if}
												<img
													src={keyFeature.gifPaths[0]}
													alt="GIF"
													on:load={() => {
														imageLoadedStates[featureIndex][0] = true;
													}}
													style:display={!imageLoadedStates[featureIndex][0] ? 'none' : 'block'}
												/>
											</div>
											<div class="desc-row">
												<ScrollArea class="h-full w-full rounded-md border">
													<div class="p-4">
														<h4 class="scroll-m-20 text-xl font-bold tracking-tight">
															{keyFeature.title}
														</h4>
														<p class="font-normal leading-7 text-gray-300">
															{keyFeature.description}
														</p>
													</div>
												</ScrollArea>
											</div>
										{/if}
									{:else}
										<div class="gif-container">
											{#each keyFeature.gifPaths as gifPath, index}
												<div class="gif">
													{#if !imageLoadedStates[featureIndex][index]}
														<Skeleton class="h-[300px] w-[500px] rounded-md" />
													{/if}
													<img
														src={gifPath}
														alt="GIF"
														on:load={() => {
															imageLoadedStates[featureIndex][index] = true;
														}}
														style:display={!imageLoadedStates[featureIndex][index]
															? 'none'
															: 'block'}
													/>
												</div>
											{/each}
										</div>
									{/if}
								</div>
							{:else}
								<div class="key-feature">
									<ScrollArea class="h-full w-full rounded-md border">
										<div class="p-4">
											<h4 class="scroll-m-20 text-xl font-bold tracking-tight">
												{keyFeature.title}
											</h4>
											<p class="font-normal leading-7 text-gray-300">
												{keyFeature.description}
											</p>
										</div>
									</ScrollArea>
								</div>
							{/if}
						{/each}

						<!-- Video if there is a path -->

						{#if videoPath !== ''}
							<div class="video">
								<video width="400" controls>
									<source src={videoPath} type="video/mp4" />
									<track kind="captions" />
									Your browser does not support the video tag.
								</video>
							</div>
						{/if}
					</div>
				</div>
			</div>
		</Dialog.Content>
	</Dialog.Root>
{:else}
	<!-- Drawer for Mobile -->
	<Drawer.Root bind:open>
		<Drawer.Trigger class={buttonVariants({ variant: 'ghost' })} style="width: 200px; height: 50px">
			See Project
		</Drawer.Trigger>
		<Drawer.Content>
			<div class="drawer-content" bind:this={dialogContent}>
				<!-- Drawer content goes here -->
				<div class="container">
					<h1 class="scroll-m-20 text-4xl font-extrabold tracking-tight lg:text-5xl">{title}</h1>
					<!-- Overview and other details -->
					<div class="card">
						<div class="overview">
							<ScrollArea class="h-full w-full rounded-md">
								<div class="p-4">
									<h4 class="text-lg font-semibold">Overview</h4>
									<p class="font-normal leading-7 text-gray-300">{overview}</p>
								</div>
							</ScrollArea>
						</div>
						{#if note !== ''}
							<div class="special" style={`background: ${noteColor}`}>
								<p>{note}</p>
							</div>
						{/if}
						{#if isSpecial === 'yes'}
							<div style="display: flex; gap: 20px; margin: 20px;">
								<Hallwaycard
									ImagePath="https://i.postimg.cc/q7cfTgdP/Lester-4x.png"
									GradientStrength={0.2}
								/>
								<Hallwaycard
									ImagePath="https://i.postimg.cc/QtbrpC4Q/Tomohide-Tseki-Plus-4x.png"
									GradientStrength={0.2}
								/>
								<Hallwaycard
									ImagePath="https://i.postimg.cc/3xv5tnfJ/Galka-World-Eater-4x.png"
									GradientStrength={0.1}
								/>
							</div>
							<div style="display: flex; gap: 20px; margin: 20px;">
								<Hallwaycard
									ImagePath="https://i.postimg.cc/hGVntpV3/AReally-Big-Rock-4x.png"
									IsStar={false}
									IsGradient={false}
								/>
								<Hallwaycard
									ImagePath="https://i.postimg.cc/Y0DKsVwj/Bob-The-Giant-4x.png"
									IsStar={false}
									IsGradient={false}
								/>
								<Hallwaycard
									ImagePath="https://i.postimg.cc/Bnrs3dPK/Toska-4x.png"
									IsStar={false}
									IsGradient={false}
								/>
							</div>
							<div style="display: flex; gap: 20px; margin: 20px;">
								<Hallwaycard
									ImagePath="https://i.postimg.cc/5tWcTLD5/Justin-4x.png"
									IsStar={false}
									IsGradient={false}
								/>
								<Hallwaycard
									ImagePath="https://i.postimg.cc/Fs1QL9jS/Dacada-4x.png"
									IsStar={false}
									IsGradient={false}
								/>
								<Hallwaycard
									ImagePath="https://i.postimg.cc/wvHpyLVx/Pugh-4x.png"
									IsStar={false}
									IsGradient={false}
								/>
							</div>
							<div style="display: flex; gap: 20px; margin: 20px;">
								<Hallwaycard
									ImagePath="https://i.postimg.cc/zDxrvLR5/Dniprokovie-4x.png"
									IsStar={false}
									IsGradient={false}
								/>
								<Hallwaycard
									ImagePath="https://i.postimg.cc/HsK10f2h/Finn-4x.png"
									IsStar={false}
									IsGradient={false}
								/>
								<Hallwaycard
									ImagePath="https://i.postimg.cc/fyRQ5sp6/Backside-4x.png"
									IsStar={false}
									IsGradient={false}
								/>
							</div>
						{/if}
						<!-- Features -->
						{#each keyFeatures as keyFeature}
							<div class={`features-and-gifs ${keyFeature.orientation}`}>
								{#if keyFeature.gifPaths.length === 1}
									{#if keyFeature.orientation === 'gif-desc'}
										<div class="gif">
											<img src={keyFeature.gifPaths[0]} alt="GIF" />
										</div>
										<div class="key-feature">
											<ScrollArea class="h-full w-full rounded-md border">
												<div class="p-4">
													<h4 class="scroll-m-20 text-xl font-bold tracking-tight">
														{keyFeature.title}
													</h4>
													<p class="font-normal leading-7 text-gray-300">
														{keyFeature.description}
													</p>
												</div>
											</ScrollArea>
										</div>
									{:else if keyFeature.orientation === 'desc-gif'}
										<div class="key-feature">
											<ScrollArea class="h-full w-full rounded-md border">
												<div class="p-4">
													<h4 class="scroll-m-20 text-xl font-bold tracking-tight">
														{keyFeature.title}
													</h4>
													<p class="font-normal leading-7 text-gray-300">
														{keyFeature.description}
													</p>
												</div>
											</ScrollArea>
										</div>
										<div class="gif">
											<img src={keyFeature.gifPaths[0]} alt="GIF" />
										</div>
									{:else if keyFeature.orientation === 'gif-desc-row'}
										<div class="gif-row">
											<img src={keyFeature.gifPaths[0]} alt="GIF" />
										</div>
										<div class="desc-row">
											<ScrollArea class="h-full w-full rounded-md border">
												<div class="p-4">
													<h4 class="scroll-m-20 text-xl font-bold tracking-tight">
														{keyFeature.title}
													</h4>
													<p class="font-normal leading-7 text-gray-300">
														{keyFeature.description}
													</p>
												</div>
											</ScrollArea>
										</div>
									{/if}
								{:else}
									{#each keyFeature.gifPaths as gifPath, index}
										{#if (index + 1) % 3 === 0}
											<div class="gif-row">
												<img src={gifPath} alt="GIF" />
											</div>
										{:else}
											<div class="gif">
												<img src={gifPath} alt="GIF" />
											</div>
										{/if}
									{/each}
									<div class="desc-row">
										<ScrollArea class="h-full w-full rounded-md border">
											<div class="p-4">
												<h4 class="scroll-m-20 text-xl font-bold tracking-tight">
													{keyFeature.title}
												</h4>
												<p class="font-normal leading-7 text-gray-300">{keyFeature.description}</p>
											</div>
										</ScrollArea>
									</div>
								{/if}
							</div>
						{/each}
						<!-- Video -->
						{#if videoPath !== ''}
							<div class="video">
								<video width="400" controls>
									<source src={videoPath} type="video/mp4" />
									<track kind="captions" />
									Your browser does not support the video tag.
								</video>
							</div>
						{/if}
					</div>
				</div>
			</div>
		</Drawer.Content>
	</Drawer.Root>
{/if}

<style>
	.special {
		background: #ffc0d9;
		color: white;
		padding: 20px;
		border-radius: 8px;
	}
	.gif-container {
		display: flex;
		flex-wrap: wrap; /* Wraps the elements to create rows */
		gap: 16px; /* Adjust the spacing between GIFs */
		margin: auto;
	}
	.dialog-content,
	.drawer-content {
		max-height: 80vh; /* Limit height to 80% of the viewport */
		overflow-y: auto; /* Enable vertical scrolling */
	}
	.container {
		display: flex;
		flex-direction: column;
		gap: 20px;
		padding: 20px;
		width: 90%; /* Adjust based on design */
		border-radius: 8px;
		max-width: 1400px;
	}
	.features-and-gifs {
		display: flex;
		gap: 10px;
		margin: 30px;
	}
	.key-feature,
	.gif,
	.gif-row,
	.desc-row {
		flex: 1;
	}
	.gif-row,
	.desc-row {
		margin-bottom: 20px;
	}

	.gif {
		flex: 0 1 calc(50% - 16px); /* Each gif takes up 50% width minus the gap */
		box-sizing: border-box; /* Makes sure padding/margins are included in the width calculation */
		margin: auto;
	}

	.gif-row {
		margin: auto; /* also center the stuff in the code below */
		align-items: center;
	}

	.gif img {
		width: 100%; /* Make sure the image fills its container */
		height: auto; /* Preserve the aspect ratio of the image */
		margin: auto;
	}
	video {
		width: 100%;
	}
</style>
