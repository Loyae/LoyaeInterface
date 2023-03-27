
<script context="module">
	//PRELOADER
    export async function load(page) {
		return { 
  			props: { 
				focus: page.params.site
			} 
		}
    }
</script>


<script>
	//import Box from '$lib/components/Box.svelte';
	import Pages from '$lib/components/Pages.svelte';
	import Button from '$lib/components/Button.svelte';
	import Table from '$lib/components/Table.svelte';
	import Tabs from '$lib/components/Tabs.svelte';
	import '../../app.css';

	//import '../scripts/dashboard.js'

	import {onMount} from 'svelte'

	let APIURL = "https://bouncy-party-production.up.railway.app"//"http://localhost:8080";


	export let focus
		

	



	// let pages = ["edx.org/search", "edx.org"]
	// let features = [];
	// for(let i=0; i < pages.length; i++){
	// 	let received = [];
	// 	onMount(async () => {
	// 		const response = await fetch(APIURL +`/stats?url=${encodeURIComponent(pages[i])}`)
	// 		received = await response.json()
			
	// 		//window.alert(received.MissingAlts)
	// 		features[i] =  received;//{page: "j", missing_alts: received.MissingAlts, meta_tags: received.FetchMeta}//construct_features(pages[i], received.MissingAlts, received.FetchMeta, received.InternalSiteSize, received.FetchAlt);
			
	// 	})
	// }

		let features = [];
		let sitemap_received
		let another_sitemap_received
		onMount(async () => {
			const focus_stat_response = await fetch(APIURL +`/stats?url=${encodeURIComponent(focus)}`)
			features[0] = await focus_stat_response.json()
			
		
			

			const sitemap = await fetch(APIURL +`/sitemap?url=${encodeURIComponent(focus)}`)
			sitemap_received = await sitemap.json()


			for(let i = 0; i < sitemap_received.Sitemap.Directs.length; i++){
				const direct_stat_response = await fetch(APIURL +`/stats?url=${encodeURIComponent(sitemap_received.Sitemap.Directs[i].Loc)}`)
				features[1+i] = await direct_stat_response.json()
			}


			//ALTERNATIVES ARN'T WORKING RN
			for(let i = 0; i < sitemap_received.Sitemap.Anothers.length; i++){
				const another_response = await fetch(APIURL +`/sitemap?xml=${encodeURIComponent(sitemap_received.Sitemap.Anothers[i].Loc)}`)
				another_sitemap_received = await another_response.json()

				for(let j = 0; j < another_sitemap_received.Sitemap.Directs.length; j++){
					const another_stat_response = await fetch(APIURL +`/stats?url=${encodeURIComponent(another_sitemap_received.Sitemap.Directs[i].Loc)}`)
					features[features.length + j] = await another_stat_response.json()
					
				}
			}

		 })
	

	
	// features[0] = {page: "▼ h", missing_alts: 5}
	// features[1] = {page: " ▼b", missing_alts: 2}


	

</script>



	<head>
		<meta name="viewport" content="width=device-width, initial-scale=1.0">
		<title>Dashboard | Loyae</title>
		  <link rel="icon" type="image/png" href="../../assets/logos/logo.png"/>
	</head>


	<h2 id="focus">{focus}</h2>

	<p> {features.length}</p>
		

		<div class="center" style="margin-top: 40px;">
			<table class="timecard">
				<caption>Diagnostic</caption>
				<thead>
					<tr>
						{#each [" ", "Title", "URL", "Missing Meta Data", "# Of Missing Alt Data"] as th}
						<th>{th}</th>
						{/each}
					</tr>
				</thead>
				<tbody>
					{#each Array(features.length) as _, i}


					<!--run loop in here-->

					<tr class="{i%2==0 ? 'even' : 'odd'}">
						<th>▶</th>
						<th>{features[i].Whois.title}</th>
						<td>{features[i].Whois.domain}</td>
						<td>{features[i].FetchMeta.description}</td>
						<td>{features[i].MissingAlts}</td>
					</tr>
					
					{/each} 
					
				
				</tbody>

			</table>

			
		</div>

	 

<style>



	

	#focus {
		margin-top: 20px;
		margin-left: 20px;
	}

	

	caption {
    border-top-right-radius: 10px;
    border-top-left-radius: 10px;
    padding: 5px;
}
    
table.timecard {
	margin: auto;
	width: 600px;
	border-collapse: collapse;
	box-shadow: 0 0 15px lightgray;
}

table.timecard caption {
	background-color: var(--active-color);
	color: #fff;
	letter-spacing: .3em;
}

table.timecard thead th {
	padding: 8px;
	background-color: white;
	font-size: large;
}

table.timecard thead th #thDay {
	width: 40%;	
}

table.timecard thead th #thRegular, table.timecard thead th#thOvertime, table.timecard thead th#thTotal {
	width: 20%;
}

table.timecard th, table.timecard td {
	padding: 3px;
	border-width: 1px;
	border-style: solid;
	border-color: var(--light-active-color) lightgray;
}

table.timecard td {
	text-align: right;
}

table.timecard tbody th {
	text-align: left;
	font-weight: normal;
}

table.timecard tr.even {
	background-color: var(--light-active-color);
}
table.timecard tr.odd {
	background-color: white;
}

</style>