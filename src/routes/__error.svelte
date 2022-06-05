<script context="module">
	export function load({ error, status }) {
		return {
			props: {
				title: `${status}: ${error.message}`
			}
		};
	}

   

</script>

<script>
	export let title;
    import Nav from '$lib/components/Nav.svelte';
	import '../app.css';

	let nav_hrefs = [["Dashboard","#"], ["Home","index.html"], ["Help","#"]];
</script>

<Nav hrefs={nav_hrefs} title={"Loyae"} logo_href={"https://www.loyae.com/assets/logos/logo.svg"}/>

<div>
Oops! The page you are looking for does not exist. It might have been moved or deleted.			
</div>