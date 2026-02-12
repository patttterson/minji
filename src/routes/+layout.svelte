<script lang="ts">
	import favicon from '$lib/assets/favicon.svg';
	import "$lib/css/fonts.css";

	let { children } = $props();
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
</svelte:head>

<style>
  :global(body) {
		font-family: 'Comfortaa', system-ui, sans-serif;
		color: white;
    background: black;
		display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
    margin: 0;
  }

	:global(::selection), :global(::-moz-selection) {
		background: #ff6ec7;
		color: black;
	}
</style>

<div>
	{@render children()}
</div>
