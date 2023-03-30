<script>
    //import Button from '$lib/components/Button.svelte';

    

    let label;
    let popup;
    //let btnll;
   

</script>

<body>



<button id="down" on:click={()=>{
                if (popup.style.display.toString()=="block"){
                    label.innerHTML = "▶"
                    popup.style.display="none";
                } else {
                    label.innerHTML = "▼"
                    popup.style.display="block";
                }}}><div id="label" bind:this="{label}">▶</div></button>
    
    <div id="popup" bind:this="{popup}" style="display:none">
        <slot></slot>
        <br/>   
    </div>
    


</body>



<style>
    button {
        border: none;
        padding: 5px;
        float: left;
    }
</style>