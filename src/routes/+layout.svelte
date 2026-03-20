<script lang="ts">
	import '$lib/css/fonts.css';
	import { dev } from '$app/environment';

	let { children } = $props();

	const title = "patty's corner" + (dev ? ' [dev]' : '');
</script>

<svelte:head>
	<meta name="viewport" content="width=device-width, initial-scale=1" />
	<title>{title}</title>
	<meta name="description" property="og:description" content="patty's personal website" />
	<link rel="icon" href="/favicon.svg" type="image/svg+xml" />
	<link rel="apple-touch-icon" sizes="180x180" href="/apple-touch-icon.png" />
	<link rel="icon" type="image/png" sizes="32x32" href="/favicon-32x32.png" />
	<link rel="icon" type="image/png" sizes="16x16" href="/favicon-16x16.png" />
	<link rel="manifest" href="/site.webmanifest" />
	<link rel="dns-prefetch" href="https://minji.love/" />
</svelte:head>

<div id="root">
	{@render children()}
</div>

<style>
	:global(body) {
		--bg-overlay-rgb: 0, 0, 0;
		--bg-dim: 0.6;
		font-family: 'Comfortaa', system-ui, sans-serif;
		background-color: black;
		background-size: cover;
		background-position: center;
		background-repeat: no-repeat;
		color: white;
		display: flex;
		justify-content: center;
		align-items: flex-start;
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

	:global(::selection),
	:global(::-moz-selection) {
		background: oklch(0.7411 0.2001 345.28);
	}

	#root {
		min-height: 100vh;
		display: flex;
		flex-direction: column;
	}
</style>
