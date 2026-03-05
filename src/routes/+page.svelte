<script lang="ts">
	import Badges from '$lib/Badges.svelte';
  import { onMount } from 'svelte';
  import madebyagirl from '$lib/assets/badges/other/madebyagirl.png';

  onMount(() => {
    // https://webneko.net/
    // @ts-ignore
    window.NekoType = "rose";
    const nekoContainer = document.createElement('h1');
    nekoContainer.id = "nl";
    const webnekoScript = document.createElement('script');
    webnekoScript.src = "https://webneko.net/n20171213.js";
    nekoContainer.appendChild(webnekoScript);
    document.body.insertBefore(nekoContainer, document.body.firstChild);
  });
</script>

<div class="header">
  <img src={madebyagirl} alt="made by a girl" class="madebyagirl badge" />
</div>
<h1 class="title">
	patty's corner
</h1>

<Badges />

<style>
  .badge {
		image-rendering: auto;
		image-rendering: crisp-edges;
		image-rendering: pixelated;
		image-rendering: -webkit-optimize-contrast;
	}
</style>