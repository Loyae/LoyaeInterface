<script>
	
	import Form from '$lib/components/Form.svelte';
	var APIURL = "https://bouncy-party-production.up.railway.app/"//"http://localhost:8080"


</script>



	<head>
		<meta name="viewport" content="width=device-width, initial-scale=1.0">
		<title>Sign In | Loyae</title>
		  <link rel="icon" type="image/png" href="../assets/logos/logo.png"/>
	</head>
<main>

<center>
<Form title={"Sign In"} prompt={"Sign In"} direct={APIURL + "/login"} class="center" APIURL={APIURL}/>
</center>

</main>


<style>
</style>