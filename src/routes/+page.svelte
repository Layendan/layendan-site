<script lang="ts">
	import IntroButton from '$lib/components/IntroButton.svelte';

	let pageIndex = 0;

	function increasePageIndex() {
		pageIndex++;
	}
</script>

{#if pageIndex === 0}
	<IntroButton on:card-click={increasePageIndex} />
{:else if pageIndex === 1}
	<span>Hello World</span>
{/if}
