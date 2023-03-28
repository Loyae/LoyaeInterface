<script>
    //import Button from '$lib/components/Button.svelte';

    

    let label = "▶"

   

</script>

<body>



<button id="down" onclick="popper()">{label}</button>
    <div id="popup" style="display:none">
        
        <slot></slot>


        <br/>


    
        
    </div>
    <script>
        
            function popper(){
                if( document.getElementById("popup").style.display.toString()=="block"){
                    document.getElementById("popup").style.display="none";
                } else {
                    document.getElementById("popup").style.display="block";

                }
            }
        
    </script>
    
    


</body>



<style>
    button {
        border: none;
        padding: 5px;
        float: left;
    }
</style>