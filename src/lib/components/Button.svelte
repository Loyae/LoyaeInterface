<script>
    export let msg;
    export let bcolor;
    export let tcolor = "black";
    export let direct;
    export let onclick;
    export let width;
    export let type;
    
</script>

{#if !onclick }
    <button style="background-color: {bcolor}; color: {tcolor}; width:{width}" href="{direct}" type="{type}">
    {msg}
    </button>
{:else if !direct}
    <button style="background-color: {bcolor}; color: {tcolor}; width:{width}" on:click={onclick} type="{type}">
    {msg}
    </button>
{:else if onclick && direct}
    <button style="background-color: {bcolor}; color: {tcolor}; width:{width}" href="{direct}" on:click={onclick} type="{type}">
    {msg}
    </button>
{:else}
    <button style="background-color: {bcolor}; color: {tcolor}; width:{width}" type="{type}">
    {msg}
    </button>
{/if}

    


<style>
    button {
        border-radius: 10px;
        border: 0;
        /*box-shadow: 0 0 5px lightcoral;*/
        padding: 10px;
    }
    
    button:hover {
       /* box-shadow: 0 0 10px lightcoral;*/
        filter: brightness(0.95);
        cursor: pointer;
    }

</style>