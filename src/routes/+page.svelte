<script lang="ts">
	type Badge =
		| {
				id: string;
				kind: 'iframe';
				src: string;
				title: string;
				style?: string;
		  }
		| {
				id: string;
				kind: 'image';
				src: string;
				alt: string;
				href?: string;
		  };

	const badges: Badge[] = [
		{ id: 'increment', kind: 'iframe', src: '//incr.easrng.net/badge?key=minji', style: 'background: url(//incr.easrng.net/bg.gif)', title: 'increment badge' },
    { id: 'sandbina', kind: 'image', src: 'sandbina.gif', alt: 'sandbina.gif', href: 'https://twitter.com/nomianims' },
		{ id: '88x31', kind: 'image', src: '88x31.png', alt: '88x31.png', href: 'https://github.com/NotNite/eightyeightthirtyone/' },
		{ id: 'vert', kind: 'image', src: 'vert.gif', alt: 'vert.gif', href: 'https://vert.minji.love/' },
		{ id: 'cobalt', kind: 'image', src: 'cobalt.gif', alt: 'cobalt.gif', href: 'https://cobalt.tools/' },
		{ id: 'wikipedia', kind: 'image', src: 'wikipedia.gif', alt: 'wikipedia.gif', href: 'https://en.wikipedia.org/wiki/User:Pattersonuwu' },
    { id: 'jellyfin', kind: 'image', src: 'jellyfin.gif', alt: 'jellyfin.gif', href: 'https://jellyfin.org/' },
		{ id: 'newjeans', kind: 'image', src: 'newjeans.gif', alt: 'newjeans.gif', href: 'https://w.wiki/HpXe/' },
    { id: 'ollie', kind: 'image', src: 'ollie.png', alt: 'ollie.png', href: 'https://ollie.lol/' },
    { id: 'mcsrranked', kind: 'image', src: 'mcsrranked.png', alt: 'mcsrranked.png', href: 'https://mcsrranked.com/stats/652a4e7f-163d-41d5-8fae-cb47f59fb12c/' },
    { id: 'osu', kind: 'image', src: 'osu.png', alt: 'osu.png', href: 'https://osu.ppy.sh/users/18741136/' },
    { id: 'tetrio', kind: 'image', src: 'tetrio.png', alt: 'tetrio.png', href: 'https://tetr.io/' },
		{ id: 'nocookie', kind: 'image', src: 'nocookie.gif', alt: 'nocookie.gif' },
    { id: 'spotify', kind: 'image', src: 'spotify.gif', alt: 'spotify.gif', href: 'https://open.spotify.com/user/3152qnqjeqtfabtkpxiekyfbhtsu/' },
    { id: 'twopaws', kind: 'image', src: 'twopaws.png', alt: 'twopaws.png', href: 'https://github.com/patttterson/minji/' },
    { id: 'scramjet', kind: 'image', src: 'scramjet.png', alt: 'scramjet.png', href: 'https://scramjet.torrent.minji.love/' },
    { id: 'uBO', kind: 'image', src: 'uBO.png', alt: 'uBO.png', href: 'https://github.com/gorhill/uBlock/' },
    { id: 'qbittorrent', kind: 'image', src: 'qbittorrent.png', alt: 'qbittorrent.png', href: 'https://qbittorrent.org/' },
		{ id: 'nyaa', kind: 'image', src: 'nyaabanner.gif', alt: 'nyaabanner.gif' },
    { id: 'bun', kind: 'image', src: 'bun.png', alt: 'bun.png', href: 'https://bun.sh/' }
	];
</script>

<h1>patty</h1>
<div class="badges">
	{#each badges as badge (badge.id)}
		{#if badge.kind === 'iframe'}
			<iframe
				src={badge.src}
				style={badge.style}
				title={badge.title}
				width="88"
				height="31"
				frameborder="0"
			></iframe>
		{:else if badge.href}
			<a class="badge-link" href={badge.href} target="_blank" rel="noopener noreferrer">
				<img class="badge" width="88" height="31" src='/88x31/{badge.src}' alt={badge.alt} />
			</a>
		{:else}
			<img class="badge" width="88" height="31" src='/88x31/{badge.src}' alt={badge.alt} />
		{/if}
	{/each}
</div>

<style>
	.badges {
		display: grid;
		grid-template-columns: auto auto auto;
		column-gap: 10px;
		row-gap: 10px;
	}

	.badge {
		image-rendering: auto;
		image-rendering: crisp-edges;
		image-rendering: pixelated;
		image-rendering: -webkit-optimize-contrast;
	}

	.badge-link {
		display: block;
    height: 31px;
	}
</style>
