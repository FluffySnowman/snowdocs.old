<script lang="ts">
	import { TableOfContents, tocCrawler } from '@skeletonlabs/skeleton';
	// import SvelteMarkdown from 'svelte-markdown';

	import { Table } from '@skeletonlabs/skeleton';
	import type { TableSource } from '@skeletonlabs/skeleton';
	import { tableMapperValues } from '@skeletonlabs/skeleton';

	import { CodeBlock } from '@skeletonlabs/skeleton';
	import hljs from 'highlight.js/lib/core';

	// codeblock highlight thing imports
	import shell from 'highlight.js/lib/languages/shell';
	import bash from 'highlight.js/lib/languages/bash';

	// register codeblock shit
	hljs.registerLanguage('shell', shell);
	hljs.registerLanguage('bash', bash);
	import 'highlight.js/styles/github-dark.css';

	import { storeHighlightJs } from '@skeletonlabs/skeleton';

	storeHighlightJs.set(hljs);

	const sourceData = [
		{ position: 1, keybind: 'Ctrl + a', explanation: 'Moves cursor to the start of the line' },
		{
			position: 2,
			keybind: 'Ctrl + e',
			explanation: 'Moves cursor to the END of the line (can also be used for autocomplete)'
		},
		{
			position: 3,
			keybind: 'Alt + b',
			explanation: 'Moves the cursor 1 word backwards (like ctrl with arrow keys)'
		},
		{
			position: 4,
			keybind: 'Alt + f',
			explanation: 'Moves the cursor 1 word forwards (like ctrl arrow keys))'
		},
		{ position: 5, keybind: 'Ctrl + p', explanation: 'Last command (up arrow)' },
		{ position: 6, keybind: 'Ctrl + n', explanation: 'Next command (like down arrow)' },
		{
			position: 7,
			keybind: 'Ctrl + w',
			explanation: 'Delete word behind (like control backspace)'
		},
		{ position: 8, keybind: 'Alt + d', explanation: 'Delet word ahead' },
		{
			position: 9,
			keybind: 'Ctrl + r',
			explanation: 'Reverse search (searching through the command history)'
		},
		{ position: 10, keybind: 'Ctrl + k', explanation: 'Delete everything to the end of the line' },
		{
			position: 11,
			keybind: 'Ctrl + u',
			explanation: 'Delete everything to the start of the line'
		},
		{
			position: 12,
			keybind: 'Ctrl + x e',
			explanation:
				'Opens your text editor with the command (you can edit a long command in vim and then run it)'
		}
	];

	const tableSimple: TableSource = {
		head: ['Shortcut', 'Explanation'],
		body: tableMapperValues(sourceData, ['keybind', 'explanation']),
		meta: tableMapperValues(sourceData, ['position', 'keybind', 'explanation'])
	};
</script>

<div use:tocCrawler={{ mode: 'generate', scrollTarget: '#page' }} class="hidden">
	<h2>CLI</h2>
	<h2>Shortcuts</h2>
	<h2>Automation</h2>
	<h3>Repository Mirroring With Crontab</h3>
</div>

<div class="flex">
	<TableOfContents class="w-2/12 p-4 sticky top-6" />

	<div class="w-8/12 p-4">
		<div id="linux-page-content" class="text-left">
			<h2 class="h1 text-[#20c20e]">CLI</h2>
			<br />
			<br />
			<h3 class="h2 text-[#FF6300] inline-flex">
				Shortcuts &nbsp; <div class="">(scrollable)</div>
			</h3>
			<br />
			<br />
			<Table source={tableSimple} class="text-sm font-mono h-64" />
			<br />
			<br />
			<hr />
			<br />
			<h3 class="h2 text-[#FFA900]">Automation</h3>
			<br />
			<h4 class="h3 text-[#ff00f0]">Repository Mirroring with Crontab</h4>
			<br />
			<div>
				<p>
					Repositories can be mirrored from one site/origin to another using just 3 commands. You
					will need read access for the Repository and write access to the new Repository. Here are
					the commands which can be put into a <code>.sh (shell script)</code> file which can be used
					for automation.
				</p>
				<br />
				<CodeBlock
					language="bash"
					lineNumbers
					code={`
# Replace the URL with your Repository
git clone --mirror https://github.com/fluffysnowman/snowdocs.git 

# Replace with your Repository
cd snowdocs.git

# Replace with the new mirror Repository's URL
git remote set-url --push origin http://192.168.1.124:8888/fluffysnowman/snowdocs.git

# Finally push the Repository
git push --mirror
				`}
				/>
				<br />
				<div id="repo-mirror-automation-wrapper">
					<p>Lets take a look at what we did here</p>
					<br />
					<div>
						<ul class="text-l">
							<li class="text-l p-1">
								<span>-</span>
								<span class="" >We cloned the github repository to a folder in our current working directory</span>
							</li>
							<li class="text-l p-1">
								<span>-</span>
								<span class="" >We changed the directory to the new repository and chaged the remote's URL to the
									one where the mirrored one will live</span >
							</li>
							<li class="text-l p-1">
								<span>-</span>
								<span class="" >We pushed the repositor to the new one with the <code>--mirror</code> option</span>
							</li>
						</ul>
					</div>
					<br />
					<p>If all went well then this should've worked</p>
					<br />
					<p>
						Now to automatically mirror the repository every 1 or 2 or x
						hours/minutes/days we can use the <code>crontab</code> on linux
					</p>
					<br />
					<p>To do this we need to open the crontab con</p>
				</div>
			</div>
		</div>
	</div>
</div>
