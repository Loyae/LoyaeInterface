<script>
	//import Box from '$lib/components/Box.svelte';
	import Pages from '$lib/components/Pages.svelte';
	import Button from '$lib/components/Button.svelte';
	import Table from '$lib/components/Table.svelte';
	import '../app.css';

	//import '../scripts/dashboard.js'

	import {onMount} from 'svelte'

	let APIURL = "http://localhost:8080";


	let focus = "example.com"


	let headers = ["Page", "Missing ALTs", "Missing Meta Tags", "Excess Bytes"];
	

	function construct_features(page, missing_alts, meta_tags, excess_bytes){
			return {
				page: page,
				missing_alts: missing_alts,
				meta_tags: meta_tags,
				excess_bytes: excess_bytes
			}
		}


	let features = [];
	for(let i=0; i < 3; i++){
		let received = [];
		onMount(async () => {
			const response = await fetch(APIURL +`/stats?url=${encodeURIComponent("edx.org")}`)
			received = await response.json()

			features[i] = construct_features("/index.html", received.MissingAlts, ["title","keywords", "description", "OG"], 1000);
			//window.alert(received.MissingAlts)
		})
	}




	

</script>



	<head>
		<meta name="viewport" content="width=device-width, initial-scale=1.0">
		<title>Dashboard | Loyae</title>
		  <link rel="icon" type="image/png" href="../assets/logos/logo.png"/>
	</head>


	<h2 id="focus">{focus}</h2>
		

	 
	  
	  <div id="tables">
		<div id="sitemap-table" class="center">
			<Table title={"Sitemaps"} ths={["URL"]}/>
		</div>


		<div id="pages-tabs">
			<div id="raw-pages-table" class="center">
				<Pages headers={headers} features={features}/>
			</div>
	
	
			<div id="cms-pages-table" class="center">
				<Table title={"CMS"} ths={["Title", "URL", "Missing Meta Data", "# Of Missing Alt Data"]}/>
			</div>
		</div>

	  </div>
	 
			
	

<!--<h1>Hello bro {name}!</h1>
<Box title={name}/>-->

<style>

	#tables {
		display: grid;
        grid-template-columns: repeat(10, 1fr);
        gap: 5px;
	}

	/*#raw-pages-table {

		grid-column: 4 / 10;
        grid-row: 3 / 4;
	}

	#cms-pages-table {
		grid-column: 2 / 3;
        grid-row: 8 / 9;
	}*/

	#pages-tabs {
		grid-column: 4 / 5;
		grid-row: 3 / 4;
	}

	#sitemap-table {
		grid-column: 2 / 3;
        grid-row: 3 / 4;
	}

	#focus {
		margin-top: 20px;
		margin-left: 20px;
	}


</style>