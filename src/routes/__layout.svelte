<script>
	import Nav from '$lib/components/Nav.svelte';
	import '../app.css';

	let nav_hrefs = [ ["Home","https://loyae.com"], ["Help","mailto:contact@loyae.com"]];

	var date = new Date();
	var yyyy = date.getFullYear();
</script>

<header>
	<Nav hrefs={nav_hrefs} title={"Loyae"} logo_href={"https://www.loyae.com/assets/logos/logo.svg"}/>
</header>


<main>
	<!--WHERE THE PAGE LOADS-->
		<slot></slot>
</main>

<footer>
	<p><b>Loyae.com</b> © {yyyy}</p>
</footer>

<style>
	header {
		position: fixed;
		width: 100%;
		top: 0;
		z-index: 999;
	}

	header + main {
  padding-top: 60px;
}
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
