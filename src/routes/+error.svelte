<script lang="ts">
	import { onMount } from 'svelte';
	import { page } from '$app/state';
	import blehh from '$lib/assets/blehh.webp';
	import vgen from '$lib/assets/vgen-logo-dark-bg.png';

	// this error page is SO FUCKING OVERENGINEERED OH MY GOD
	let errorCodeEl: HTMLHeadingElement;
	let errorMessageEl: HTMLHeadingElement;
	let errorLineEl: HTMLDivElement;
	let artistCreditEl: HTMLDivElement;
	let stacked = false;
	let artistCreditNaturalWidth = 0;

	const updateLayout = () => {
		if (!errorLineEl || !errorCodeEl || !errorMessageEl) return;
		const gap = 32;
		// clamp(220px, 85vw, 520px)
		const width = Math.min(Math.max(220, window.innerWidth * 0.85), 520);
		const codeWidth = errorCodeEl.scrollWidth;
		const messageWidth = errorMessageEl.scrollWidth;
		stacked = width < codeWidth + messageWidth + gap;
		if (!stacked) {
			stacked = width < artistCreditNaturalWidth;
		}
	};

	onMount(() => {
		artistCreditNaturalWidth = artistCreditEl.scrollWidth;
		updateLayout();
		window.addEventListener('resize', updateLayout);
		return () => window.removeEventListener('resize', updateLayout);
	});

	const mdnUrl = `https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/${page.status}`;
</script>

<div class="error-container" class:stacked>
	<div class="artist-credit" class:stacked bind:this={artistCreditEl}>
		<span class="nowrap">error image by</span>
		<span class="nowrap"
			><enhanced:img src={vgen} class="vgen-logo" alt="vgen logo" />/<a
				class="author"
				href="https://vgen.co/Sukebunn"
				target="_blank"
				rel="noopener noreferrer">Sukebunn</a
			></span
		>
	</div>
	{#if stacked}
		<h1 id="error-code" style="margin-bottom: .5em;" bind:this={errorCodeEl}>
			<a href={mdnUrl} target="_blank" rel="noopener noreferrer">{page.status}</a>
		</h1>
	{/if}
	<img src={blehh} class="error-image" alt="Error" />
	<div class="error-line" class:stacked bind:this={errorLineEl}>
		{#if !stacked}
			<h1 id="error-code" bind:this={errorCodeEl}>
				<a href={mdnUrl} target="_blank" rel="noopener noreferrer">{page.status}</a>
			</h1>
		{/if}
		<h1 id="error-message" bind:this={errorMessageEl}>{page.error?.message}</h1>
	</div>
</div>

<style>
	.error-container {
		--error-img-width: clamp(220px, 85vw, 520px);
		flex: 1;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	.error-container.stacked {
		align-items: flex-start;
	}

	.vgen-logo {
		width: 3rem;
		height: auto;
		margin: 0;
		vertical-align: middle;
		position: relative;
		top: -2px;
	}

	.nowrap {
		white-space: nowrap;
	}

	.author {
		font-family: 'Satoshi', system-ui, sans-serif;
		font-weight: 840;
	}

	.artist-credit.stacked {
		position: absolute;
		top: 1.5rem;
		left: 50%;
		transform: translateX(-50%);
		text-align: center;
	}

	.artist-credit {
		margin-bottom: 1rem;
		font-size: 1.5rem;
	}

	.error-image {
		width: var(--error-img-width);
		height: calc(var(--error-img-width) / 2);
		box-sizing: border-box;
		border: 4px solid white;
		background-color: oklch(0.8461 0.0647 316.95);
	}

	.error-line {
		width: var(--error-img-width);
		display: flex;
		align-items: baseline;
		gap: 1rem;
	}

	.error-line.stacked {
		justify-content: flex-start;
	}

	#error-message {
		margin-left: auto;
		text-align: right;
		max-width: 100%;
		overflow-wrap: anywhere;
		word-break: break-word;
		white-space: normal;
	}

	.error-line.stacked #error-message {
		margin-left: 0;
		text-align: left;
	}

	a {
		color: inherit;
		text-decoration: none;
	}

	a:hover {
		text-decoration: underline;
	}
</style>
