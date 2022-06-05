<script>
    export let msg;
    export let bcolor;
    export let tcolor = "black";
    
</script>

<button style="background-color: {bcolor}; color: {tcolor};">
{msg}
</button>


<style>
    button {
        border-radius: 5px;
        border: 0;
        box-shadow: 0 0 15 lightgray;
        padding: 10px;
    }
    
    button:hover {
        box-shadow: 0 0 15 gray;
        filter: brightness(0.85);
        cursor: pointer;
    }

</style>