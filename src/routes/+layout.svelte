<script lang="ts">
	import '../app.postcss';
	import { AppShell, AppBar } from '@skeletonlabs/skeleton';
	// Floating UI for Popups
	import { computePosition, autoUpdate, flip, shift, offset, arrow } from '@floating-ui/dom';
	import { storePopup } from '@skeletonlabs/skeleton';
	storePopup.set({ computePosition, autoUpdate, flip, shift, offset, arrow });

	// START ===== AUTOCOMPLETE SEARCH OPTIONS (SEARCHBAR THING)

	import { Autocomplete } from '@skeletonlabs/skeleton';
	import type { AutocompleteOption } from '@skeletonlabs/skeleton';
	import type { PopupSettings } from '@skeletonlabs/skeleton';
	import { popup } from '@skeletonlabs/skeleton';

	const searchOptions: AutocompleteOption<string>[] = [
		{
			label: 'Linux',
			value: 'Cool shit',
			keywords: 'linux, cli, command, shell',
			meta: { pageLink: '/linux' }
		},
		{
			label: 'Cyber Security',
			value: 'hacking',
			keywords: 'hacking, hack, cyber, security, command, aircrack, crack',
			meta: { pageLink: '/sec' }
		}
	];

	let popupSettings: PopupSettings = {
		event: 'focus-click',
		target: 'popupAutocomplete',
		placement: 'bottom'
	};

	let inputPopup: string = '';

	function onSearchSelection(event: CustomEvent<AutocompleteOption<string>>): void {
		inputPopup = event.detail.label;
		// console.log(event.detail.meta.pageLink);
		const pageToNavigateTo: string = event.detail.meta.pageLink;
		console.log(pageToNavigateTo);
	}

	// END ===== AUTOCOMPLETE SEARCH OPTIONS (SEARCHBAR THING)
</script>

<!-- The app shell thing -->
<AppShell slotSidebarLeft="bg-surface-500/5 w-56 p-4" regionPage="scroll-smooth">
	<svelte:fragment slot="header">
		<!-- top navbar shit -->
		<AppBar>
			<svelte:fragment slot="lead">
				<strong class="text-2xl font-thin">SnowDocs</strong>
			</svelte:fragment>

			<div id="searchBar" class="w-2/12 absolute top-2 right-24">
				<input
					class="input autocomplete"
					type="search"
					name="autocomplete-search"
					bind:value={inputPopup}
					placeholder="Search..."
					use:popup={popupSettings}
				/>

				<div data-popup="popupAutocomplete" class="bg-purple-800 opacity-10 w-64">
					<Autocomplete
						bind:input={inputPopup}
						options={searchOptions}
						on:selection={onSearchSelection}
					/>
				</div>
			</div>

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
