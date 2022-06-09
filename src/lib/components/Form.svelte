<script>
    export let title;
    export let prompt;
    export let direct;
    
    
	import Button from '$lib/components/Button.svelte';
</script>


<div id="form">
    <h3>{title}</h3>

    <Button bcolor={"var(--active-color)"} tcolor={"white"} msg={prompt} direct={direct} />
</div>


<style>
    #form {
        box-shadow: 0 0 15px lightgray;
        position: relative;
        justify-content: center;
        border-radius: 15px;
        
        margin-top: 40px;
        height: 600px;
        width: 400px;
    }

  

</style>