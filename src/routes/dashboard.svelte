<script>
	//import Box from '$lib/components/Box.svelte';
	import Pages from '$lib/components/Pages.svelte';
	import Button from '$lib/components/Button.svelte';
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
		

	 
	  
	  
	 
			<div id="table" class="center">
			<Pages headers={headers} features={features}/>
			</div>
	
			<div id="optimize-all-btn" class="center">
			<Button bcolor={"var(--active-color)"} msg={"Optimize All"}/>
			</div>
	
	  
	  
	  
	  
	 
			<table style="width:100px">
				CMS
				<tr>
				  <th>Title</th>
				  <th>URL</th>
				  <th>Meta Description</th>
				</tr>
				<tr>
				  <td>Emil</td>
				  <td>Tobias</td>
				  <td>check</td>
				</tr>
				<tr>
				  <td>16</td>
				  <td>14</td>
				  <td>X</td>
				</tr>
			  </table>

		


		
		
	

<!--<h1>Hello bro {name}!</h1>
<Box title={name}/>-->

<style>

	

	#table {
		margin-top: 20%;
	}

	#optimize-all-btn {
		margin-top: 1%;
	}


	#focus {
		margin-top: 20px;
		margin-left: 20px;
	}

	table, th, td,tr {
		border:1px solid black;
		margin: 0;
		padding:0;
	}


</style>