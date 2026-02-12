<script lang="ts">
	import favicon from '$lib/assets/favicon.svg';
	import "$lib/css/fonts.css";
	import { onMount } from 'svelte';

	import background from '$lib/assets/background.webp';

	let { children } = $props();

	onMount(() => {
		document.body.style.backgroundImage = `url(${background})`;
	});
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
</svelte:head>


<style>
  :global(body) {
		--bg-overlay-rgb: 0, 0, 0;
		--bg-dim: 0.6;
		font-family: 'Comfortaa', system-ui, sans-serif;
		background-size: cover;
		background-position: center;
		background-repeat: no-repeat;
		color: white;
		display: flex;
		justify-content: center;
		align-items: center;
		min-height: 100vh;
		margin: 0;
  }

	:global(body)::before {
		content: '';
		position: fixed;
		inset: 0;
		background: rgba(var(--bg-overlay-rgb), var(--bg-dim));
		pointer-events: none;
		z-index: -1;
	}

	:global(::selection), :global(::-moz-selection) {
		background: #ff6ec7;
		color: black;
	}
</style>

<div>
	{@render children()}
</div>
