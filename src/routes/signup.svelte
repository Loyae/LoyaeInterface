<script>
	
	import Form from '$lib/components/Form.svelte';
	var APIURL = "https://bouncy-party-production.up.railway.app"//"http://localhost:8080"

</script>



	<head>
		<meta name="viewport" content="width=device-width, initial-scale=1.0">
		<title>Sign Up | Loyae</title>
		  <link rel="icon" type="image/png" href="../assets/logos/logo.png"/>
	</head>
<main>

<center>
<Form title={"Sign Up"} prompt={"Sign Up"} direct={APIURL +"/register"} class="center" APIURL={APIURL}/>
</center>

</main>


<style>
</style>


		