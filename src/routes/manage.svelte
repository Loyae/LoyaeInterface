<script>
	import '../app.css';
	//import fetchFaviconAndBanner from '../scripts/app.js'
	
	let sitelist = ["Loyae.com", "Elldel.com", "Example.com", "Gooooooooogle.com", "Youtube.com", "hi.com"]

	
</script>

<head>
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>Manage | Loyae</title>
	<link rel="icon" type="image/png" href="../assets/logos/logo.png"/>
</head>

<main>

	<div id="site-list">
		{#each sitelist as site}
			<a href="/dashboard/{site}" sveltekit:prefetch>
				<div class="block">
					<img src="https://github.githubassets.com/favicons/favicon.png" alt="site favicon" class="site-favicon"/>

					<span>{site}</span> 

				
				</div>
			</a>
		{/each}

		<a href="/">
			<div class="block" id="new-site">
				<span>+</span>
			</div>
		</a>
		

	</div>

<br/>
</main>

<style>

#site-list {
	background-color: var(--light-active-color);
	
}
#site-list a {
	text-decoration: none;
}

.block {
	background-color: var(--active-color);
	display: inline-flex;
	height: 200px;
	width: 200px;
	overflow: hidden;
	box-shadow: 0px 0px 15px lightgray;
}

.block:hover {
	filter: brightness(0.95);
        cursor: pointer;
}

.block span {
	font-weight: bold;
	font-size: large;
	color: white;
	margin-left: 30px;
}
	

#site-list, .block {
	border-radius: 10px;
	padding: 30px;
	margin: 30px;
}

#new-site span{
	text-align: center;
	font-size: 100px;
	vertical-align: middle;
	
}

#new-site{
    align-items: center;
}



.site-favicon {
	position: absolute;
	-webkit-filter: drop-shadow(0px 0px 15px var(--light-active-color));
  	filter: drop-shadow(0px 0px 15px var(--light-active-color));

	height: 20px;
}




</style>


