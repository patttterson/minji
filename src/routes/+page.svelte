<script lang="ts">
	import Badges from '$lib/Badges.svelte';
  import { onMount } from 'svelte';

  // https://webneko.net/
  onMount(() => {
    window.NekoType = "rose";

    const nekoContainer = document.createElement('h1');
    nekoContainer.id = "nl";
    const webnekoScript = document.createElement('script');
    webnekoScript.src = "https://webneko.net/n20171213.js";
    nekoContainer.appendChild(webnekoScript);
    document.body.insertBefore(nekoContainer, document.body.firstChild);
  })
</script>

<h1>patty's corner</h1>

<Badges />