<script lang="ts">
	import { TableOfContents, tocCrawler } from '@skeletonlabs/skeleton';
	// import SvelteMarkdown from 'svelte-markdown';

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

<div use:tocCrawler={{ mode: 'generate', scrollTarget: '#page' }} class="hidden">
	<h2>Wireless Network Auditing</h2>
	<h3>Installation</h3>
	<h3><a href="#wifi-attacks-with-aircrack">WiFi Attacks with Aircrack</a></h3>
</div>

<div class="flex">
	<div class="w-2/12 p-4 sticky top-6">
		<TableOfContents class="sticky top-6" />
	</div>

	<div class="w-8/12 p-4">
		<div id="sec-page-content" class="text-left">
			<h2 class="h1 text-[#20c20e]">Wireless Network Auditing</h2>
			<br />
			<p><b>(copy pasting everything from the old site)</b></p>
			<br />
			<h2 class="h2 text-[#20c20e]">Installation</h2>

			<br />
			<p>
				First we'll start with basic network security testing and mapping. Common tools used for
				this are:
			</p>
			<br />
			<ul class="list-disc pl-5 font-mono">
				<li>aircrack-ng</li>
				<li>wireshark</li>
				<li>nmap</li>
				<li>airgeddon</li>
				<li>etherape</li>
				<li>mtr</li>
				<li>tcpdump</li>
				<li>traceroute</li>
			</ul>
			<br />
			<CodeBlock
				language="shell"
				lineNumbers
				code={`aircrack-ng wireshark nmap airgeddon etherape mtr tcpdump traceroute net-tools
`}
			/>

			<br />
			<p>
				Above are some of the tools that beginners use to crack, map and track wireless and wired
				networks. For these examples we will be using a debian distribution of linux such as Ubuntu,
				Parrot or Kali. So you gotta load up these tools on your computer now. You can use the
				advanced package tool `apt` to install these tools.
			</p>

			<br />
			<CodeBlock
				language="shell"
				lineNumbers
				code={`sudo apt-get update

sudo apt-get install aircrack-ng wireshark nmap airgeddon etherape host mtr tcpdump traceroute net-tools
`}
			/>

			<br />
			<h2 id="wifi-attacks-with-aircrack" class="h2 text-[#20c20e]">WiFi Attacks with Aircrack</h2>
			<br />

			<p>
				So... Now you decide you wanna test your wireless network's security. Lets jump right into
				it! Tools which we'll be using for this are the `aircrack-ng` suite. These can be used to
				put your networking device into monitor mode, scan for wireless networks around you and
				finally.. crack them. Let's start this by firing up a temrinal.
				<br />
				<br />
				<b
					>You will need to be a superuser/admin to use these commands so make sure you have a root
					terminal open or use `su` or `sudo su` to do so.
				</b>
				<br />
				<br />

				<CodeBlock language="shell" lineNumbers code={`ifconfig`} />
				<br />

				This command will show all your wireless and wired interfaces for networks that your
				computer has access to. You will have to select a wireless interface. The default value for
				a wireless interface on linux usually starts with `wl` (Example: `wlan0`(standing for
				'Wireless Local Area Network #0'). The output should look a little something like this:
			</p>

			<br />
		</div>
	</div>
</div>
