<script context="module">
export async function load({ url }) {
    return {props:{focus: url.searchParams.get('url')}};
}
  </script>

<script>
	console.log("START")
	//import { page } from '$app/stores';
	//import { page } from '$app/stores';
	//PRELOADER
    // export async function load() {
		
	// 	return { 
  	// 		props: { 
	// 			focus: page.searchParams.get("url")
	// 		} 
	// 	};
    // }

// 	export let page;
//   const searchParams = new URLSearchParams(page.query);
//   const focus = searchParams.get('url');
	


	//import Box from '$lib/components/Box.svelte';
	// import Pages from '$lib/components/Pages.svelte';
	// import Button from '$lib/components/Button.svelte';
	// import Table from '$lib/components/Table.svelte';
	// import Tabs from '$lib/components/Tabs.svelte';
	import Drop from '$lib/components/Drop.svelte';
	import Countdown from '$lib/components/Countdown.svelte';
	import '../app.css';
	

	
  //import Countdown from '../lib/components/Countdown.svelte';
	

	//import '../scripts/dashboard.js'

	import {onMount} from 'svelte'

	let APIURL = "https://api.loyae.com"//"http://localhost:8080";

	export let focus
	//export let focus

	

	
		// const waitlist_button = document.getElementById("waitlist_button");
					// waitlist_button.addEventListener("click", joinwaitlist());
					
					function joinwaitlist() {
						//alert(document.getElementById('waitlist_email').value)
						if(document.getElementById('waitlist_email').value==""){
							alert("Please enter your name and email, then try again.")
						}

						fetch("https://api.loyae.com/waitlist?name="+document.getElementById('waitlist_name').value+"&email="+document.getElementById('waitlist_email').value+"&url="+focus, {"method":"GET"}).then(response=>{
									document.getElementById("waitlist_button").style.backgroundColor="lightgray";
									document.getElementById("waitlist_button").innerHTML = "Joined!"
								}).catch(err=>{
									window.alert("Please enter your name and email, then try again.")
								})
							
									
					}




		
	   
	
			
		 
	



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
		let MAX_DIAG = 30;

		let features = [];
		let sitemap_received
		let another_sitemap_received

		onMount(async () => {
			console.log("INSIDE")
			const focus_stat_response = await fetch(APIURL +`/stats?url=${encodeURIComponent(focus)}`)
			features[0] = await focus_stat_response.json()
			
		
			

			const sitemap = await fetch(APIURL +`/sitemap?url=${encodeURIComponent(focus)}`)
			sitemap_received = await sitemap.json()


			for(let i = 0; i < sitemap_received.Sitemap.Directs.length; i++){
				if(features.length >= MAX_DIAG){
					break;
				}
				const direct_stat_response = await fetch(APIURL +`/stats?url=${encodeURIComponent(sitemap_received.Sitemap.Directs[i].Loc)}`)
				features[1+i] = await direct_stat_response.json()
			}


			//ALTERNATIVES ARN'T WORKING RN
			// for(let i = 0; i < sitemap_received.Sitemap.Anothers.length; i++){
			// 	const another_response = await fetch(APIURL +`/sitemap?xml=${encodeURIComponent(sitemap_received.Sitemap.Anothers[i].Loc)}`)
			// 	another_sitemap_received = await another_response.json()

			// 	for(let j = 0; j < another_sitemap_received.Sitemap.Directs.length; j++){
			// 		if(features.length >= MAX_DIAG){
			// 			break;
			// 		}
			// 		const another_stat_response = await fetch(APIURL +`/stats?url=${encodeURIComponent(another_sitemap_received.Sitemap.Directs[i].Loc)}`)
			// 		features[features.length + j] = await another_stat_response.json()
					
			// 	}
			// }

		 })
	

	console.log(features[0])
	// features[0] = {page: "▼ h", missing_alts: 5}
	// features[1] = {page: " ▼b", missing_alts: 2}


	const header=["Title", "URL", "Missing Image ALT Text", "Meta Description", "Meta Keywords", "OG Meta Tags"/*, "Supplementary & 3rd Party Meta Tags"*/]

</script>



	<head>
		<meta name="viewport" content="width=device-width, initial-scale=1.0">
		<title>Dashboard | Loyae</title>
		  <link rel="icon" type="image/png" href="../../assets/logos/logo.png"/>
	</head>


	<div class="center" id="info-panel">
		
			<div id="favicon-display">
				{#if features.length >= 1 && features[0].Whois.favicon != "" && features[0].Whois.favicon.length >= 4} 
					<img src="{features[0].Whois.favicon}" height="30px"/>
				{/if}
			</div>
			<h2 id="focus-display">{focus}</h2>
		

		
		<div>
			<div>
				<input type="text" id="waitlist_name" name="waitlist_name" placeholder="name">
				<input type="text" id="waitlist_email" name="waitlist_email" placeholder="email">
				<button on:click|once={joinwaitlist} id="waitlist_button">Join Waitlist</button>
				
			</div> 

			
				<!-- <Countdown FontSize="12"/> -->
				<br/>
				<div>  <b>API & Wordpress Plugin Releases In </b>
				<!-- <b>{countdown_days} days : {countdown_hours} hours : {countdown_minutes} minutes : {countdown_seconds} seconds</b> -->
				<Countdown date="july 6, 2023 01:30:00"/>
				</div>
	   
			
		</div>


		<!-- <h2>
			Wordpress Plugin Comming Soon
		</h2> -->
	</div>
		
		
							

		<div class="center" id="info-table">
			<table class="timecard">
				
				<caption>
					{#if features.length == 0}
					<div class="loader"></div>
					{/if}
					Diagnostic ({features.length})</caption>
				<thead>
					<tr>
						{#each header as th}
							{#if th === "URL"}
								<th style="width: 10px; word-wrap: break-word;">{th}</th> <!--NOT WORKING-->
							{:else}
							<th>{th}</th>
							{/if}
						
						{/each}
					</tr>
				</thead>
				<tbody>
					<th style="background-color: lightgray;" colspan="{header.length}"><center>{focus}</center></th>
					{#each Array(features.length) as _, i}


					<!--run loop in here-->

					<tr class="{i%2==0 ? 'even' : 'odd'}">
						<th><b>{features[i].Whois.title}</b></th>
						<td><a href="{`http://`+features[i].Whois.domain}">{features[i].Whois.domain}</a></td>
						<td>
							Missing <b>
								{#if features[i].MissingAlts != 0}
									<span style="color:red">{features[i].MissingAlts}</span>
								{:else}
									<span style="color:green">{features[i].MissingAlts}</span>
								{/if}
							
							</b> alt attributes out of
							{#if features[i].FetchAlt != null}{features[i].FetchAlt.length}{:else}NA{/if} total images</td>

						<td><b>{#if features[i].FetchMeta.description == ""}
							<span style="color: red">Missing</span>
							{:else}
							<span style="color: green">Exists</span>
							{/if}</b>
						</td>
						<td><b>{#if (typeof features[i].FetchMeta.keywords != 'undefined')}
								 {#if features[i].FetchMeta.keywords.split(",").length < 10}<span style="color:red">{features[i].FetchMeta.keywords.split(",").length}/10</span>{:else}<span style="color:green">{features[i].FetchMeta.keywords.split(",").length}/10</span>{/if}
							{:else}
								<span style="color: red;">0/10</span>
							{/if}
							</b>
							Keywords
						</td>
						
						<td>
							{#if (typeof features[i].FetchMetaOG.description != 'undefined') && features[i].FetchMetaOG.description == ""}
							<span style="color: red">Missing og:description</span><br/>
							{:else}
							<span style="color: green">Has og:description</span><br/>
							{/if}
							{#if (typeof features[i].FetchMetaOG.image != 'undefined') && features[i].FetchMetaOG.image == ""}
							<span style="color: red">Missing og:image</span><br/>
							{:else}
							<span style="color: green">Has og:image</span><br/>
							{/if}
							{#if (typeof features[i].FetchMetaOG.site_name != 'undefined') && features[i].FetchMetaOG.site_name == ""}
							<span style="color: red">Missing og:site_name</span><br/>
							{:else}
							<span style="color: green">Has og:site_name</span><br/>
							{/if}
							{#if (typeof features[i].FetchMetaOG.title != 'undefined') && features[i].FetchMetaOG.title == ""}
							<span style="color: red">Missing og:title</span><br/>
							{:else}
							<span style="color: green">Has og:title</span><br/>
							{/if}
							{#if (typeof features[i].FetchMetaOG.url != 'undefined') && features[i].FetchMetaOG.url == ""}
							<span style="color: red">Missing og:url</span><br/>
							{:else}
							<span style="color: green">Has og:url</span><br/>
							{/if}
						</td>
						<!-- <td>
							FOR NONESSENTIAL TAGS
						</td> -->
					</tr>
					<th colspan="{header.length}" class="{i%2==0 ? 'even' : 'odd'}">
						<Drop>
							<center>
							<!-- <p>Size: {features[i].InternalSiteSize} Bytes</p>-->
							<br/> 
							<p><b>Speed:</b> {features[i].RequestSpeed} Nanosecond</p>
							<br/>
							<p><b>Meta description:</b> 
								{#if features[i].FetchMeta.description}
								{features[i].FetchMeta.description}
								{:else}
								<span style="color: red">Does not exist</span>
								{/if}
							
							</p>
							<br/>
							<p><b>Meta Keywords: </b>
								{#if features[i].FetchMeta.keywords}
								{features[i].FetchMeta.keywords}
								{:else}
								<span style="color: red">Does not exist</span>
								{/if}
							
							</p>
							<br/>
							<p><b>OG Meta description: </b>
								{#if features[i].FetchMetaOG.description}
								{features[i].FetchMetaOG.description}
								{:else}
								<span style="color: red">Does not exist</span>
								{/if}
							
							</p>
							<br/>
							<p><b>OG Meta image:</b> </p> 

								{#if features[i].FetchMetaOG.image}
									<img src="{features[i].FetchMetaOG.image}" height="200px" alt="og"/>
								{:else}
									<span style="color: red">Does not exist</span>
								{/if}

							<br/><br/>
							<p><b>OG Site Name:</b>
								{#if features[i].FetchMetaOG.site_name}
									{features[i].FetchMetaOG.site_name}
								{:else}
									<span style="color: red">Does not exist</span>
								{/if}

							 </p>
							<br/>
							<!-- <p>Import Sizes: </p><br/>
							<p>CSS: {features[i].FetchImportSizes.CSSSize}</p><br/>
							<p>IFrame: {features[i].FetchImportSizes.IFRAMESize}</p><br/>
							<p>Image: {features[i].FetchImportSizes.IMAGESize}</p><br/>
							<p>JS: {features[i].FetchImportSizes.JSSize}</p><br/> -->
							<div>
								<b>Images:</b>
								<div style="max-height: 250px; overflow:auto;">
								<table style="border: solid black 1px;">
									{#if features[i].FetchAlt != null}
										{#each features[i].FetchAlt as img}
											<tr>
												<th><img src="{img[0]}" alt="{img[2]}" height="50px"/></th>
													{#if img[2]}
													<th>{img[2]}</th>
													{:else}
													<span style="color: red">No alt data</span>
													{/if}
												

											</tr>
										{/each}
										{:else}
										<span style="color: red">No Images</span>
									{/if}
								</table>
								</div>
							</div>
						</center>
						</Drop>
					</th>

					{#if i == 0 && features.length > 1}
					<tr>
					<td style="background-color: lightgray;" colspan="{header.length}"><center>Other Pages</center></td>	
					</tr>
					
					{/if}
					<!--ELSE: Say, "No sitemap, generate one with loyae"-->
					
					{/each} 
					
					
				
				</tbody>

			</table>
			<br/>
					
		</div>

		{#if features.length >= MAX_DIAG}
						<div style="color: red" colspan="{header.length}" class="center">
							<b>MAX # OF ROWS PER SESSION REACHED ({MAX_DIAG})</b>
						</div>
					{/if}

			<br/>
			<br/>
			<center>
				<p>Crawl A New Page: </p><br/>
			</center>

			<div  class="center">
				<input type="text" id="new-url-input" placeholder="example.com" />
				<!-- <button onclick="newpage()" type="submit" class="shadow-hover search-buttons">Launch</button> -->
				<button onclick="newpage()">DIAGNOSE</button>
				
				<script>
					function newpage(){
						window.open("http://"+window.location.host + '/diagnose?url=' + document.getElementById('new-url-input').value, '_blank');
					}
				</script>
			</div>


	 

<style>

@media only screen and (max-width: 800px) {

	#focus-display{
		display: none;
	}
	#favicon-display{
		display: none;
	}
}

#info-panel {
	width: 85%;
	margin-top: 20px;
	position:relative;
	text-align: left;
	justify-content: left;
}

#favicon-display{
	margin-right: 5px;
	vertical-align: middle;
}

#focus-display {
	margin-right: 10%
}
#info-table{
	margin-top: 40px; 
	max-height: 650px;
	overflow: auto;
	width: 85%;
	
}


.loader {
  border: 6px solid white;
  border-radius: 50%;
  border-top: 6px solid lightcoral;
  width: 20px;
  height: 20px;
  -webkit-animation: spin .8s linear infinite;
  /* Safari */
  animation: spin .8s linear infinite;
  display: block;
  margin:0;
  float: left;
}

@-webkit-keyframes spin {
  0% {
    -webkit-transform: rotate(0deg);
  }
  100% {
    -webkit-transform: rotate(360deg);
  }
}

@keyframes spin {
  0% {
    -webkit-transform: rotate(0deg);
            transform: rotate(0deg);
  }
  100% {
    -webkit-transform: rotate(360deg);
            transform: rotate(360deg);
  }
}

input[type=text]{
	margin-right: 10px;
	padding: 10px; 
	border: none; 
	background-color: var(--light-active-color); 
	border-radius:10px
}

button, input[type=submit] {
	border-radius: 10px; 
	border: none; 
	background-color: var(--active-color);
	color: white; 
	border-radius: 10px; 
	padding: 10px
       
    }
    
    button:hover {
       /* box-shadow: 0 0 10px lightcoral;*/
        filter: brightness(0.95);
        cursor: pointer;
	}
	



	

	caption {
		border-top-right-radius: 10px;
		border-top-left-radius: 10px;
		padding: 5px;
	}
    
table.timecard {
	margin: auto;
	width: 100%;
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


table.timecard th, table.timecard td {
	padding: 3px;
	border-width: 1px;
	border-left-style: solid;
	border-color: var(--light-active-color) lightgray;
}

table.timecard td {
	text-align: left;
	font-size: 1.1em;
	padding-left: 10px;
}

table.timecard tbody th {
	text-align: left;
	font-weight: normal;
	font-size: 1.1em;
	padding-left: 10px;
}

table.timecard tr.even, th.even {
	background-color: var(--light-active-color);
}
table.timecard tr.odd, th.odd{
	background-color: white;
}

</style>