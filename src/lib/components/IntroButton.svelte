<script lang="ts">
	import { createEventDispatcher } from 'svelte';

	const subtitle = "Welcome to my website! Let's see some cool stuff! 🚀";

	let card: HTMLButtonElement;

	const dispatcher = createEventDispatcher();

	function handleCardClick() {
		card.style.setProperty('transform', 'scale(10)');
		card.style.setProperty('opacity', '0');
		// Set >= than transition duration
		setTimeout(() => dispatcher('card-click'), 500);
	}
</script>

<button class="custom-card" bind:this={card} on:click|once={handleCardClick}>
	<div class="custom-card-content">
		<h3 class="custom-card-title">Aidan Labourdette</h3>
		<h4 class="custom-card-subtitle">
			{#each subtitle.split(' ') as string, index}
				<span style="transition-delay: {index * 40}ms" class="custom-card-subtitle-word">
					{string}
				</span>
			{/each}
		</h4>
	</div>
</button>

<style lang="postcss">
	.custom-card {
		aspect-ratio: 1.6 / 1;
		border: 0.5vmin solid theme(colors.primary);
		@apply cursor-pointer relative h-[80vmin] transition-all duration-500;
	}

	.custom-card:hover:before {
		background-position: 100% 100%;
		transform: scale(1.08, 1.03);
	}

	.custom-card:hover > .custom-card-content {
		background-position: -10% 0%;
	}

	.custom-card:hover > .custom-card-content > .custom-card-subtitle > .custom-card-subtitle-word {
		@apply opacity-100 translate-y-0;
		transition: opacity 0ms, transform 200ms cubic-bezier(0.9, 0.06, 0.15, 0.9);
	}

	.custom-card:before {
		background: linear-gradient(
			130deg,
			transparent 0% 33%,
			theme(colors.primary) 66%,
			theme(colors.secondary) 83.5%,
			theme(colors.accent) 100%
		);
		background-position: 0% 0%;
		background-size: 300% 300%;
		content: '';
		height: 100%;
		left: 0px;
		pointer-events: none;
		position: absolute;
		top: 0px;
		transition: background-position 350ms ease, transform 350ms ease;
		width: 100%;
		z-index: 1;
	}

	.custom-card-content {
		background-image: radial-gradient(theme(colors.base-100/0.2) 8%, transparent 8%);
		background-position: 0% 0%;
		background-size: 5vmin 5vmin;
		transition: background-position 350ms ease;
		@apply h-full p-[5vmin] relative w-full z-10 items-center flex flex-col justify-center;
	}

	.custom-card-title,
	.custom-card-subtitle {
		@apply text-white font-normal m-0;
		font-family: 'Anek Latin', sans-serif;
	}

	.custom-card-title {
		font-size: 6vmin;
	}

	.custom-card-subtitle {
		font-size: 3vmin;
		margin-top: 2vmin;
	}

	.custom-card-subtitle-word {
		display: inline-block;
		margin: 0vmin 0.3vmin;
		opacity: 0;
		position: relative;
		transform: translateY(40%);
		transition: none;
	}
</style>
