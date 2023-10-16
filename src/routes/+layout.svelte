<script>
	import '../app.postcss';
	import { AppShell, AppBar } from '@skeletonlabs/skeleton';
	// Floating UI for Popups
	import { computePosition, autoUpdate, flip, shift, offset, arrow } from '@floating-ui/dom';
	import { storePopup } from '@skeletonlabs/skeleton';
	storePopup.set({ computePosition, autoUpdate, flip, shift, offset, arrow });
</script>

<!-- The app shell thing -->
<AppShell slotSidebarLeft="bg-surface-500/5 w-56 p-4" regionPage="scroll-smooth">
	<svelte:fragment slot="header">
		<!-- top navbar shit -->
		<AppBar>
			<svelte:fragment slot="lead">
				<strong class="text-2xl font-thin">SnowDocs</strong>
			</svelte:fragment>
			<svelte:fragment slot="trail">
				<a
					class="btn btn-sm variant-ghost-surface"
					href="https://github.com/fluffysnowman/snowdocs"
					target="_blank"
					rel="noreferrer"
				>
					GitHub
				</a>
			</svelte:fragment>
		</AppBar>
	</svelte:fragment>

	<svelte:fragment slot="sidebarLeft">
		<!-- sidebar navbar list -->
		<nav class="list-nav">
			<ul>
				<li><a href="/">Home</a></li>
				<li><a href="/general">General</a></li>
				<li><a href="/linux">Linux</a></li>
				<li><a href="/sec">Cyber Security</a></li>
			</ul>
		</nav>
		<!-- --- -->
	</svelte:fragment>

	<!-- Page Route shit -->

	<slot />

	<!-- end of page router -->

</AppShell>
