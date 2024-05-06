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

	

		let MAX_DIAG = 50;
		let superficial_len = 0;
		let features = [];
		let sitemaps = [];
		let done_loading = false;

		onMount(async () => {
			console.log("INSIDE")
			const focus_stat_response = await fetch(APIURL +`/stats?url=${encodeURIComponent(focus)}`)
			features[0] = await focus_stat_response.json()
				
			if(features[0].Err == true){
					window.alert("Error fetching your website. Please try again.")
				}
			
			
			superficial_len+=1;
			

			const sitemap = await fetch(APIURL +`/sitemap?url=${encodeURIComponent(focus)}`)
			sitemaps[0] = await sitemap.json()

			for(let i = 0; i < ((sitemaps[0].Sitemap.Anothers != null) ? sitemaps[0].Sitemap.Anothers.length : 0); i++){
				if(superficial_len >= MAX_DIAG){
					break;
				}
				const another_response = await fetch(APIURL +`/sitemap?xml=${encodeURIComponent(sitemaps[0].Sitemap.Anothers[i].Loc)}`)
				let temp = await another_response.json()
				superficial_len+= ((temp.Sitemap.Directs != null) ? temp.Sitemap.Directs.length : 0);
				sitemaps.push(temp)
				console.log(temp)
				
			}

			
				for(let s = 0; s < sitemaps.length; s++){
					
							for(let i = 0; i < ((sitemaps[s].Sitemap.Directs != null) ? sitemaps[s].Sitemap.Directs.length : 0); i++){
								console.log("HERE: ", i, ": ", sitemaps[s].Sitemap.Directs.length)
								if(features.length >= MAX_DIAG){
									break;
								}
								const direct_stat_response = await fetch(APIURL +`/stats?url=${encodeURIComponent(sitemaps[s].Sitemap.Directs[i].Loc)}`)
								await direct_stat_response.json()
								.then((resp)=> {
									features[features.length]=resp
									console.log(resp)
									console.log(i)
									
								})
								
								
							}
				}
			

				done_loading = true;
			

		 })

	// console.log(features[0])
	// features[0] = {page: "▼ h", missing_alts: 5}
	// features[1] = {page: " ▼b", missing_alts: 2}


	const header=["Title", "URL", "Missing Image Alt Text", "Meta Description", "Open Graph Meta Tags", "Other Tags"/*, "Supplementary & 3rd Party Meta Tags"*/]
	


  function goToPluginPage() {
    fetch("https://api.loyae.com/logquery?log=" + encodeURIComponent(window.location.search));
	window.location.href = 'https://wordpress.org/plugins/loyae/';
  }




</script>



	<head>
		<meta name="viewport" content="width=1024">
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
					<button on:click|once={()=>(goToPluginPage())} id="waitlist_button">WordPress Plugin ➤</button>
				</div>
	   			
			
		


		<!-- <h2>
			Wordpress Plugin Comming Soon
		</h2> -->
	</div>
		
		
							

		<div class="center" id="info-table">
			<table class="timecard">
				
				<caption>
					{#if done_loading==false && (typeof features[0] != 'undefined' && features[0].Err == false)}
					<div class="loader"></div>
					{/if}
					Diagnostic ({features.length})</caption>
				<thead>
					<tr>
						{#each header as th}
							<th>{th}</th>
						
						{/each}
					</tr>
				</thead>
				<tbody>
					<th style="background-color: lightgray;" colspan="{header.length}"><center>{focus}</center></th>
					{#each Array(features.length) as _, i}


					<!--run loop in here-->

					<tr class="{i%2==0 ? 'even' : 'odd'}">
						<th width="35px" style="word-wrap: break-word;"><b>{features[i].Whois.title}</b></th>

						<td><div style="width: 150px;word-wrap: break-word; overflow: hidden;"><a href="{`http://`+features[i].Whois.domain}">{features[i].Whois.domain}</a></div></td>
						<td>
							Missing <b>
								{#if features[i].MissingAlts != 0}
									<span style="color:red; font-size: 30px;">{features[i].MissingAlts}</span>
								{:else}
									<span style="color:green">{features[i].MissingAlts}</span>
								{/if}
							
							</b> alt attributes out of
							{#if features[i].FetchAlt != null}{features[i].FetchAlt.length}{:else}NA{/if} total images</td>

						<td><b>{#if features[i].FetchMeta.description == "" || !features[i].FetchMeta.description}
							<span style="color: red; font-size: 20px;">Missing</span>
							{:else}
							<span style="color: green">Exists</span>
							{/if}</b>
						</td>
						
						
						<td>
							{#if (typeof features[i].FetchMetaOG['og:description'] == 'undefined') || features[i].FetchMetaOG['og:description'] == ""}
							<span style="color: red">Missing og:description</span><br/>
							{:else}
							<span style="color: green">Has og:description</span><br/>
							{/if}
							
							{#if (typeof features[i].FetchMetaOG['og:image'] == 'undefined') || features[i].FetchMetaOG['og:image'] == ""}
							<span style="color: red">Missing og:image</span><br/>
							{:else}
							<span style="color: green">Has og:image</span><br/>
							{/if}

							{#if (typeof features[i].FetchMetaOG['og:image:alt'] == 'undefined') || features[i].FetchMetaOG['og:image:alt'] == ""}
							<span style="color: red">Missing og:image:alt</span><br/>
							{:else}
							<span style="color: green">Has og:image:alt</span><br/>
							{/if}

							{#if (typeof features[i].FetchMetaOG['og:image:width'] == 'undefined') || features[i].FetchMetaOG['og:image:width'] == ""}
							<span style="color: red">Missing og:image:width</span><br/>
							{:else}
							<span style="color: green">Has og:image:width ({features[i].FetchMetaOG['og:image:width']})</span><br/>
							{/if}

							{#if (typeof features[i].FetchMetaOG['og:image:height'] == 'undefined') || features[i].FetchMetaOG['og:image:height'] == ""}
							<span style="color: red">Missing og:image:height</span><br/>
							{:else}
							<span style="color: green">Has og:image:height ({features[i].FetchMetaOG['og:image:height']})</span><br/>
							{/if}

							{#if (typeof features[i].FetchMetaOG['og:image:type'] == 'undefined') || features[i].FetchMetaOG['og:image:type'] == ""}
							<span style="color: red">Missing og:image:type</span><br/>
							{:else}
							<span style="color: green">Has og:image:type ({features[i].FetchMetaOG['og:image:type']})</span><br/>
							{/if}
							
							{#if (typeof features[i].FetchMetaOG['og:site_name'] == 'undefined') || features[i].FetchMetaOG['og:site_name'] == ""}
							<span style="color: red">Missing og:site_name</span><br/>
							{:else}
							<span style="color: green">Has og:site_name</span><br/>
							{/if}
							
							{#if (typeof features[i].FetchMetaOG['og:title'] == 'undefined') || features[i].FetchMetaOG['og:title'] == ""}
							<span style="color: red">Missing og:title</span><br/>
							{:else}
							<span style="color: green">Has og:title</span><br/>
							{/if}
							
							{#if (typeof features[i].FetchMetaOG['og:url'] == 'undefined') || features[i].FetchMetaOG['og:url'] == ""}
							<span style="color: red">Missing og:url</span><br/>
							{:else}
							<span style="color: green">Has og:url</span><br/>
							{/if}

							{#if (typeof features[i].FetchMetaOG['og:type'] == 'undefined') || features[i].FetchMetaOG['og:type'] == ""}
							<span style="color: red">Missing og:type</span><br/>
							{:else}
							<span style="color: green">Has og:type</span><br/>
							{/if}
							

							{#if (typeof features[i].FetchMetaOG['og:keywords'] == 'undefined') || features[i].FetchMetaOG['og:keywords'] == ""}
							<span style="color: red">Missing og:keywords</span><br/>
							{:else}
							<span style="color: green;">Has <b>{features[i].FetchMeta.keywords.split(",").length}</b> og:keywords</span><br/>
							{/if}
							 
					   </td>

					   <td>
							{#if (typeof features[i].FetchMeta.keywords == 'undefined') || features[i].FetchMeta.keywords == ""}
							<span style="color: red">Missing keywords</span><br/>
							{:else}
							<span style="color: green;">Has <b>{features[i].FetchMeta.keywords.split(",").length}</b> keywords</span><br/>
							{/if}
							
							{#if (typeof features[i].FetchMeta['theme-color'] == 'undefined') || features[i].FetchMeta['theme-color'] == ""}
							<span style="color: red">Missing theme-color</span><br/>
							{:else}
							<span style="color: green;">Has theme-color: <span style="color:{features[i].FetchMeta['theme-color']};">{features[i].FetchMeta['theme-color']}</span></span><br/>
							{/if}

							{#if (typeof features[i].FetchCanonical == 'undefined')}
							<span style="color: red">Missing canonical tag</span><br/>
							{:else}
							<span style="color: green;">Has canonical tag</span><br/>
							{/if}

							{#if (typeof features[i].FetchMeta.viewport == 'undefined')  || features[i].FetchMeta.viewport == ""}
							<span style="color: red">Missing viewport</span><br/>
							{:else}
							<span style="color: green;">Has viewport</span><br/>
							{/if}


							{#each ["twitter:card","twitter:title","twitter:description","twitter:image","twitter:image:alt", "twitter:url", "apple-mobile-web-app-status-bar-style", "apple-mobile-web-app-title"] as t}
								{#if (typeof features[i].FetchMeta[t] == 'undefined')  || features[i].FetchMeta[{t}] == ""}
								<span style="color: red">Missing {t}</span><br/>
								{:else}
								<span style="color: green;">Has {t}</span><br/>
								{/if}
							{/each}

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
							<p><b>Speed:</b> {features[i].RequestSpeed} nanoseconds</p>
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
								{#if features[i].FetchMetaOG['og:description']}
								{features[i].FetchMetaOG['og:description']}
								{:else}
								<span style="color: red">Does not exist</span>
								{/if}
							
							</p>
							<br/>
							<p><b>OG Meta image:</b> </p> 

								{#if features[i].FetchMetaOG['og:image']}
									<img src="{features[i].FetchMetaOG['og:image']}" height="200px" alt="og"/>
								{:else}
									<span style="color: red">Does not exist</span>
								{/if}

							<br/><br/>
							<p><b>OG Site Name:</b>
								{#if features[i].FetchMetaOG['og:site_name']}
									{features[i].FetchMetaOG['og:site_name']}
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
							<!-- <button on:click={MAX_DIAG+=20}>More</button> -->
							<b>MAX # OF ROWS PER SESSION REACHED ({MAX_DIAG})</b>
						</div>
		{/if}

		<br/>

		<center><p style="font-size: 20px;">Want to add this missing metadata into your site? Install the <b>WordPress plugin</b> to add it automatically using AI!</p><br/>
		
			<div>
				<button on:click|once={()=>(goToPluginPage())} id="waitlist_button">WordPress Plugin ➤</button>
			</div>
		<br/>
			Don't use WordPress? Join the <b>waitlist</b> to be notified when the plugin for other CMS platforms are released (Wix, Webflow, Squarespace, Shopify, and more...)
		<br/><br/>
		<div>
			<input type="text" id="waitlist_name" name="waitlist_name" placeholder="name">
			<input type="text" id="waitlist_email" name="waitlist_email" placeholder="email">
			<button on:click|once={joinwaitlist} id="waitlist_button">Join</button>
			
		</div> 
		<style>
  #download {
        background-color: lightcoral; 
        padding: 20px; 
        border: 0; 
        box-shadow: 0 0 15px lightcoral; 
        color: white; 
        text-decoration: none; 
        border-radius: 10px;
    }
    #download:hover {
        box-shadow: 0 0 20px lightcoral; 
    }
		</style>

		
			<!-- <Countdown FontSize="12"/> -->
			<br/>
			
		</center>

			<br/>
			<br/>
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
