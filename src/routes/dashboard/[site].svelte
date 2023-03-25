
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


	//let focus = "example.com"

	export let focus
		



	//let headers = ["Page", "Missing ALTs", "Missing Meta Tags", "Excess Bytes"];
	

	function construct_features(page, missing_alts, meta_tags, site_size, fetch_alt){
			return {
				page: page,
				missing_alts: missing_alts,
				meta_tags: meta_tags,
				site_size: site_size,
				fetch_alt: fetch_alt,
				//site_size: site_size
			}
		}
		//window.alert("1");
	let pages = ["edx.org/search", "edx.org"]
	let features = [];
	for(let i=0; i < pages.length; i++){
		let received = [];
		onMount(async () => {
			const response = await fetch(APIURL +`/stats?url=${encodeURIComponent(pages[i])}`)
			received = await response.json()
			
			//window.alert(received.MissingAlts)
			features[i] =  received;//{page: "j", missing_alts: received.MissingAlts, meta_tags: received.FetchMeta}//construct_features(pages[i], received.MissingAlts, received.FetchMeta, received.InternalSiteSize, received.FetchAlt);
			
		})
	}

	
	// features[0] = {page: "▼ h", missing_alts: 5}
	// features[1] = {page: " ▼b", missing_alts: 2}


	

</script>



	<head>
		<meta name="viewport" content="width=device-width, initial-scale=1.0">
		<title>Dashboard | Loyae</title>
		  <link rel="icon" type="image/png" href="../../assets/logos/logo.png"/>
	</head>


	<h2 id="focus">{focus}</h2>
		

	  
	  

		

		
		<div class="center" style="margin-top: 40px;">
			
				<!-- <div id="raw-pages-table" class="center, tab-content">
					<Pages headers={headers} features={features}/>
				</div> -->
		
		
				
					<Table title={"Diagnostic"} ths={[" ", "Title", "URL", "Missing Meta Data", "# Of Missing Alt Data"]} data={features}/>
				
			
				
			
		</div>

	 
			
	

<!--<h1>Hello bro {name}!</h1>
<Box title={name}/>-->

<style>



	

	#focus {
		margin-top: 20px;
		margin-left: 20px;
	}

	

</style>