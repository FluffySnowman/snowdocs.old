<script lang="ts">
	import { TableOfContents, tocCrawler } from '@skeletonlabs/skeleton';
	// import SvelteMarkdown from 'svelte-markdown';

	import { Table } from '@skeletonlabs/skeleton';
	import type { TableSource } from '@skeletonlabs/skeleton';
	import { tableMapperValues } from '@skeletonlabs/skeleton';

	// import { CodeBlock } from '@skeletonlabs/skeleton';
	import hljs from 'highlight.js/lib/core';

	// codeblock highlight thing imports
	import xml from 'highlight.js/lib/languages/xml'; // for HTML
	import css from 'highlight.js/lib/languages/css';
	import json from 'highlight.js/lib/languages/json';
	import javascript from 'highlight.js/lib/languages/javascript';
	import typescript from 'highlight.js/lib/languages/typescript';
	import shell from 'highlight.js/lib/languages/shell';

	// register codeblock shit
	hljs.registerLanguage('xml', xml); // for HTML
	hljs.registerLanguage('css', css);
	hljs.registerLanguage('json', json);
	hljs.registerLanguage('javascript', javascript);
	hljs.registerLanguage('typescript', typescript);
	hljs.registerLanguage('shell', shell);
	import 'highlight.js/styles/github-dark.css';

	import { storeHighlightJs } from '@skeletonlabs/skeleton';

	storeHighlightJs.set(hljs);

	const sourceData = [
		{ position: 1, keybind: 'Ctrl + a', explanation: 'Moves cursor to the start of the line' },
		{
			position: 2,
			keybind: 'Ctrl + e',
			explanation: 'Moves cursor to the END of the line (can also be used for autocomplete)'
		}
	];

	const tableSimple: TableSource = {
		head: ['Shortcut', 'Explanation', 'Test Column'],
		body: tableMapperValues(sourceData, ['keybind', 'explanation']),
		meta: tableMapperValues(sourceData, ['position', 'keybind', 'explanation'])
	};
</script>

<div use:tocCrawler={{ mode: 'generate', scrollTarget: '#page' }} class="hidden">
	<h2>CLI</h2>
	<h2>Shortcuts</h2>
	<h3>Automation</h3>
</div>

<div class="flex">
	<TableOfContents class="w-2/12 p-4 sticky top-6" />

	<div class="w-8/12 p-4">
		<div id="linux-page-content" class="text-left">
			<h2 class="h1 text-[#20c20e]">CLI</h2>
			<br />
			<br />
			<h3 class="h2 text-[#FF6300]">Shortcuts</h3>
			<br />
			<Table source={tableSimple} />
			<br />
			<br />
			<hr />

			<h3 class="h2 text-[#FFA900]">Automation</h3>
		</div>
	</div>
</div>
