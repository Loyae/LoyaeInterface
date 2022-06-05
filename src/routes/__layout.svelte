<script>
	import Nav from '$lib/components/Nav.svelte';
	import '../app.css';

	let nav_hrefs = [["Dashboard","#"], ["Home","index.html"], ["Help","#"]];
</script>


<Nav hrefs={nav_hrefs} title={"Loyae"} logo_href={"https://www.loyae.com/assets/logos/logo.svg"}/>


<footer>
	<p>(c) Loyae from Lins Technologies</p>
</footer>

<style>
	footer {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		padding: 40px;
	}


	@media (min-width: 480px) {
		footer {
			padding: 40px 0;
		}
	}
</style>
