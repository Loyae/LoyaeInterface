
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

	let APIURL = "http://localhost:8080";


	//let focus = "example.com"

	export let focus
		



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
		  <link rel="icon" type="image/png" href="../../assets/logos/logo.png"/>
	</head>


	<h2 id="focus">{focus}</h2>
		

	 <div id="panel">
		<a>Sitemap</a> <br/>
		<a>Settings</a> <br/>

	 </div>
	  
	  

		

		
		<div id="pages-tabs" class="center">
			<Tabs tabs={[{title: "HTML", id: "raw-pages-table"}, {title: "CMS", id: "cms-pages-table"}, {title: "Sitemap", id: "sitemap-table"}]} >
			
				<div id="raw-pages-table" class="center, tab-content">
					<Pages headers={headers} features={features}/>
				</div>
		
		
				<div id="cms-pages-table" class="center, tab-content">
					<Table title={"CMS"} ths={["Title", "URL", "Missing Meta Data", "# Of Missing Alt Data"]}/>
				</div>
			
				<div id="sitemap-table" class="center, tab-content">
					<Table title={"Sitemaps"} ths={["URL"]}/>
				</div>
				
			</Tabs>
		</div>

	 
			
	

<!--<h1>Hello bro {name}!</h1>
<Box title={name}/>-->

<style>

	#raw-pages-table{width: 300px;}
	#cms-pages-table{width: 300px;}



	#pages-tabs {
		margin-top: 40px;
	}

	

	#focus {
		margin-top: 20px;
		margin-left: 20px;
	}

	#panel {
		float: left;
		clear: left;
		display: block;
		box-shadow: 0 0 15px lightgray;
		background-color: var(--light-active-color);
		margin-top: 40px;
		height: 200%;
		border-top-right-radius: 10px;
		width: 200px;
		position: absolute;
		padding: 30px;
	}

</style>