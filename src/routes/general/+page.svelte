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
	<h2>Networking Basics</h2>
	<h3>Netmsks</h3>
	<h3>DHCP</h3>
	<h3>DNS</h3>
	<h3>Actual test</h3>
	<h3>yeet</h3>
	<h2>Heading 3</h2>
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
			<p>
				Networking is a simple yet complex part of the computing experience. It is essentially the
				connection between computers (phones and tablets included) and servers. The communication
				between these computers and servers is done through a network. Transmission of data (in
				packets) is done through a network. A network consists of many things. First thing is an IP
				(Internet Protocol) Address that is an address that tells the router on the network which
				computer is which. Learn how to change your IP Address [here](#change-your-ip). Sometimes
				people set up routers and firewalls to bind IP Addresses and MAC (Media Access Control)
				addresses. A MAC address is the address/hexadecimal code that identifies the ID of your NIC
				(Network Interface Card). Most people don't change MAC IDs or don't know how to. You can
				learn how to do this [here](#change-your-mac-address). The Default configuration for
				routers' gateways are `192.168.1.1`. A gateway is the network node through all traffic
				travels through to the WWW (World Wide Web) or another IP/MAC on your network. You can
				change the settings in the network to send data from IP to IP instead of routing it through
				the gateway too but that is a bit complicated and we will leave it for later.
			</p>
			<br />
			<p>
				Each router has a certain amount of devices(IPs) that can connect to it. This is determined
				by the 1/24 or 0/24 added at the end of the gateway IP also known as netmask. IP calculators
				are the easier way of determining how many devices are allowed. For Example: A network with
				netmask of `/24` will allow up to 254 devices at a time however a network with netmask of
				`/23` will allow 510 devices at a time.
			</p>

			<br />

<CodeBlock language="ts" code={`const skeleton: string = 'awesome';`}></CodeBlock>
			<!-- <SvelteMarkdown {source} /> -->

		</div>
	</div>
</div>
