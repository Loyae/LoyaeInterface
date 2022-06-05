<script>
	//import Box from '$lib/components/Box.svelte';
	import Table from '../lib/components/Table.svelte';
	import Button from '$lib/components/Button.svelte';
	import '../app.css';


	import {onMount} from 'svelte'

	let APIURL = "http://localhost:8080";





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
		  <link rel="stylesheet" type="text/css" href="../styles/dashboard.css"/>
		  <link rel="stylesheet" type="text/css" href="../styles/gauge.css"/>
		  <script src="../scripts/main.js"></script>
		  <script src="../scripts/dashboard.js"></script>
		  <link rel="icon" type="image/png" href="../assets/logos/logo.png"/>
	</head>



		


		<div id="table" class="center">
		<Table headers={headers} features={features}/>
		</div>

		<div id="optimize-all-btn" class="center">
		<Button bcolor={"var(--active-color)"} msg={"Optimize All"}/>
		</div>


		
	

<!--<h1>Hello bro {name}!</h1>
<Box title={name}/>-->

<style>

	.center {
		margin-left: auto;
		margin-right: auto;
		margin-top: 3px;
		margin-bottom: 3px;
		text-align: center;
		display: flex;
		justify-content: center;
	}

	#table {
		margin-top: 20%;
	}

	#optimize-all-btn {
		margin-top: 1%;
	}






</style>