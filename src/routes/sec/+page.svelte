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
	import bash from 'highlight.js/lib/languages/bash';

	// Register each imported language module
	hljs.registerLanguage('xml', xml); // for HTML
	hljs.registerLanguage('css', css);
	hljs.registerLanguage('json', json);
	hljs.registerLanguage('javascript', javascript);
	hljs.registerLanguage('typescript', typescript);
	hljs.registerLanguage('shell', shell);
	hljs.registerLanguage('bash', bash);
	import 'highlight.js/styles/github-dark.css';

	import { storeHighlightJs } from '@skeletonlabs/skeleton';

	storeHighlightJs.set(hljs);
</script>

<div use:tocCrawler={{ mode: 'generate', scrollTarget: '#page' }} class="hidden">
	<h2>Wireless Network Auditing</h2>
	<h3>Installation</h3>
	<h3>WiFi Attacks with Aircrack</h3>
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

			<div>
				So... Now you decide you wanna test your wireless network's security. Lets jump right into
				it! Tools which we'll be using for this are the `aircrack-ng` suite.
				<p>
					These can be used to put your networking device into monitor mode, scan for wireless
					networks around you and finally.. crack them. Let's start this by firing up a temrinal.
				</p>

				<br />

				<p>
					<b>
						You will need to be a superuser/admin to use these commands so make sure you have a root
						terminal open or use `su` or `sudo su` to do so.
					</b>
					<br />
					<br />
				</p>
				<CodeBlock language="shell" lineNumbers code={`ifconfig`} />
				<br />

				<p>
					This command will show all your wireless and wired interfaces for networks that your
					computer has access to. You will have to select a wireless interface. The default value
					for a wireless interface on linux usually starts with <code>wl</code> (Example:
					<code>wlan0</code> (standing for 'Wireless Local Area Network #0').
				</p>
			</div>

			<div>
				<br />
				<p>
					<b
						>NOTE: YOU WILL NEED TO MAKE SURE THAT YOUR WIFI ADAPTER ALLOWS 'MONITOR MODE' TO WORK
						WITH THE NEXT TOOL.
					</b>

					<br />
					Once you have found your wireless adapter name, you need to put it in monitor mode to look
					for (monitor) networks. This is done by typing the following command:
					<br />
					<br />
					<CodeBlock
						language="bash"
						lineNumbers
						code={`
airmon-ng check kill
airmon-ng start <interface name>

#Example: 
airmon-ng check kill
airmon-ng start wlan0
				`}
					/>

					<br />
				</p>
				<p>
					Airmon-ng will check if the wireless adapter is already in monitor mode and if it is it
					will kill it. Then it will start the adapter in monitor mode. So now we have our wireless
					card in monitor mode. Time to scan for some networks! The command airodump-ng will scan
					for wireless networks around you. But you will have to specify a wireless network
					interface for it to scan with.
				</p>
				<br />
				<CodeBlock
					language="bash"
					lineNumbers
					code={`
airodump-ng <interface name> 
#Example: 
airodump-ng wlan0`}
				/>

				<br />
				<br />
				<div>
					<p>
						This basically lists all the wireless networks' MAC ID's (BSSID) and their channel. It
						also lists the BSSIDs of the devices connected to it (station).
					</p>
					<br />
					<h2 class="h2 text-[#20c20e]">Deauthentication</h2>
					<br />
					<p>
						Now what you gotta do to get a .cap file (caplet) is create a handshake between a device
						joining the network and the network itself. To do this you have to kick a device off the
						network using the STATION MAC ID (station). and the BSSID of the network shown next to
						it (BSSID). You will also have to write this data to a .cap file for cracking later.
						Note the BSSID of the router, the channel that its on and the STATION MAC ID to kick off
						the network. Also note down the name of the file you want to save the .cap to. Now you
						will have to run aireplay-ng while airodump-ng is running as you have to capture a
						handshake- not just kick someone off the wifi. Follow these steps and replace the
						respective values in brackets with the values you got from the airodump-ng output.
					</p>
					<br />
					<span class="text-l font-bold">Window 1:</span>
					<br />
					<CodeBlock
						language="bash"
						lineNumbers
						code={`
airodump-ng --bssid <ACCESS POINT BSSID> -c <CHANNEL> -w <FILENAME> <INTERFACE NAME>
				`}
					/>
					<br />
					<span class="text-l font-bold">Window 2:</span>
					<br />
					<CodeBlock
						language="bash"
						lineNumbers
						code={`
aireplay-ng -0 0 -a <ACCESS POINT BSSID> -c <STATION MAC ID> <INTERFACE NAME>
				`}
					/>

					<br />
					<p>
						Now you have to wait for aireplay-ng to do its job. (If you get any problems with these
						commands feel free to [leave a comment](#comments-section)) If all of this is
						successful, you should see a line like this at the top of the airodump-ng window:
					</p>
				</div>
				<br />
				<b
					>NOTE: When kicking devices off the network to get a handshake, you should be mindful that
					anyone could be logging the network and their computer's connection to the network so it
					is wise to change your MAC Address everytime you boot or everytime you do a deauth attack.
					Leant how to [Change Your MAC Address
					here](https://fluffysnowman.github.io/jekyll/update/2022/04/17/main.html#change-your-mac-address)</b
				>
			</div>

			<br />
		</div>
	</div>
</div>
