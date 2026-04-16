<script lang="ts">
	import '@fortawesome/fontawesome-free/css/all.min.css';

	import Badges from '$lib/Badges.svelte';
	import { onMount } from 'svelte';
	import madebyagirl from '$lib/assets/badges/other/madebyagirl.png';
	import angelnumbers from '$lib/assets/badges/other/angelnumbers.png';

	onMount(() => {
		// https://webneko.net/
		// @ts-expect-error: too lazy to make nekotypes
		window.NekoType = 'rose';
		const nekoContainer = document.createElement('h1');
		nekoContainer.id = 'nl';
		const webnekoScript = document.createElement('script');
		webnekoScript.src = 'https://webneko.net/n20171213.js';
		nekoContainer.appendChild(webnekoScript);
		document.body.insertBefore(nekoContainer, document.body.firstChild);
	});
</script>

<div class="badges-container">
	<Badges />
	<div class="other-badges">
		<img src={madebyagirl} alt="made by a girl" class="madebyagirl badge" />
		<img src={angelnumbers} alt="angel numbers" class="angelnumbers badge" />
	</div>
</div>

<div class="content">
	<h1 class="title mb-0">patty's corner</h1>
	<p>dumb idiot that sucks at web development and loves newjeans (#newjeansisfive)</p>

	<h2 class="mb-0">Projects</h2>
	<p class="projects-subtitle">thats about it i got like nothing completed</p>
	<div class="projects">
		<div class="project-card minji">
			<a
				class="project-main-link"
				href="https://minji.love"
				target="_blank"
				rel="noopener noreferrer"
				aria-label="minji"
			></a>
			<span class="project-name">minji</span>
			<span class="project-desc">this website</span>
			<a
				class="project-github"
				href="https://github.com/patttterson/minji"
				target="_blank"
				rel="noopener noreferrer"
				aria-label="github source"><i class="fab fa-github"></i></a
			>
		</div>
		<div class="project-card asumi">
			<a
				class="project-main-link"
				href="https://minji.love/s"
				target="_blank"
				rel="noopener noreferrer"
				aria-label="asumi"
			></a>
			<span class="project-name">asumi</span>
			<span class="project-desc">link shortener</span>
			<a
				class="project-github"
				href="https://github.com/patttterson/asumi"
				target="_blank"
				rel="noopener noreferrer"
				aria-label="github source"><i class="fab fa-github"></i></a
			>
		</div>
	</div>
</div>

<style>
	.content {
		display: flex;
		flex-direction: column;
		align-items: flex-start;
		width: min(1000px, 75%);
		margin: 0 auto;
	}

	.mb-0 {
		margin-bottom: 0;
	}

	.badge {
		image-rendering: auto;
		image-rendering: crisp-edges;
		image-rendering: pixelated;
		image-rendering: -webkit-optimize-contrast;
	}

	.badges-container {
		width: 95%;
		margin: 0 auto;
	}

	.other-badges {
		display: flex;
		align-items: center;
		justify-content: center;
		gap: 10px;
	}

	.projects-subtitle {
		opacity: 0.6;
		font-size: 0.9rem;
	}

	.projects {
		display: flex;
		flex-wrap: wrap;
		gap: 12px;
		width: 100%;
	}

	.project-card {
		position: relative;
		display: flex;
		flex-direction: column;
		gap: 2px;
		padding: 12px 48px 12px 16px;
		border-radius: 10px;
		background: rgba(255, 255, 255, 0.07);
		border: 1px solid rgba(255, 255, 255, 0.12);
		text-decoration: none;
		color: inherit;
		transition:
			background 0.15s,
			border-color 0.15s,
			transform 0.1s;
		min-width: 160px;
	}

	.project-card:hover {
		background: rgba(255, 255, 255, 0.13);
		border-color: rgba(255, 255, 255, 0.25);
		transform: translateY(-2px);
	}

	.project-main-link {
		position: absolute;
		inset: 0;
		border-radius: 10px;
		z-index: 0;
	}

	.project-name {
		font-weight: 700;
		font-size: 1rem;
		pointer-events: none;
	}

	.project-desc {
		font-size: 0.8rem;
		opacity: 0.6;
		pointer-events: none;
	}

	.project-card.minji .project-name {
		color: oklch(0.7411 0.2001 345.28);
	}

	.project-card.asumi .project-name {
		color: oklch(0.9031 0.0468 261.36);
	}

	.project-github {
		position: absolute;
		top: 50%;
		right: 12px;
		transform: translateY(-50%);
		color: rgba(255, 255, 255, 0.5);
		font-size: 1.2rem;
		text-decoration: none;
		transition: color 0.15s;
		line-height: 1;
		z-index: 1;
	}

	.project-github:hover {
		color: white;
	}
</style>
