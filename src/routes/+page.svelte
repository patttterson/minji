<script lang="ts">
	import Badges from '$lib/Badges.svelte';
  import FlickeringText from '$lib/FlickeringText.svelte';
  import { onMount } from 'svelte';

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

<FlickeringText text="patty's corner" />

<Badges />