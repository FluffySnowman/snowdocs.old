<script lang="ts">
	import { TableOfContents, tocCrawler } from '@skeletonlabs/skeleton';
	import SvelteMarkdown from 'svelte-markdown';

import { CodeBlock } from '@skeletonlabs/skeleton';
import hljs from 'highlight.js/lib/core';

// Import each language module you require
import xml from 'highlight.js/lib/languages/xml'; // for HTML
import css from 'highlight.js/lib/languages/css';
import json from 'highlight.js/lib/languages/json';
import javascript from 'highlight.js/lib/languages/javascript';
import typescript from 'highlight.js/lib/languages/typescript';
import shell from 'highlight.js/lib/languages/shell';

// Register each imported language module
hljs.registerLanguage('xml', xml); // for HTML
hljs.registerLanguage('css', css);
hljs.registerLanguage('json', json);
hljs.registerLanguage('javascript', javascript);
hljs.registerLanguage('typescript', typescript);
hljs.registerLanguage('shell', shell);
import 'highlight.js/styles/github-dark.css';

import { storeHighlightJs } from '@skeletonlabs/skeleton';

storeHighlightJs.set(hljs);
			
</script>

<div use:tocCrawler={{ mode: 'generate' }} class="hidden">
	<h2>Nothing Here</h2>
	<h3>test</h3>
	<p>...</p>
</div>

<div class="flex">
	<div class="w-2/12 p-4 sticky top-6">
		<TableOfContents />
	</div>

	<div class="w-8/12 p-4">
		<div id="general-page-content" class="text-left">
			<h1>Networking Basics</h1>
			<br />
			<p><b>(copy pasting everything from the old site)</b></p>
			<br />

			<br />

<!-- <CodeBlock language="ts" code={`const skeleton: string = 'awesome';`}></CodeBlock> -->
			<!-- <SvelteMarkdown {source} /> -->

		</div>
	</div>
</div>
