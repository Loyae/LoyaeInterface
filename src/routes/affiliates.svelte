<script>
    import Button from '$lib/components/Button.svelte';
    import Popup from '../lib/components/popup.svelte';
</script>

<head>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Affiliate Program | Loyae</title>
      <link rel="icon" type="image/png" href="../assets/logos/logo.png"/>
</head>

<main>
<h1 class="center">Loyae Affiliate Program</h1>
<br/>

<div class="center">
    Earn 25% of the revenue for the first 10 days from new user activity!

</div>
<br/>
<div class="center">
    <Button msg="Apply" bcolor="var(--active-color)" onclick="affiliateForm()"/>
</div>

<Popup>Sign Up!!!</Popup>


</main>


<style>
main {
    margin-top: 30px;
}

</style>