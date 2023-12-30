<script>
import Button from './Button.svelte';
//export let page_titles = ["/index.html", "/about.html"];
export let headers;
export let features;



</script>




<table>
    <tr>
        {#each headers as heading}    
            <th><span>{heading}</span></th>
        {/each}

        <th colspan=2><Button msg="Optimize All - $20" bcolor={"var(--active-color)"}/></th>
    </tr>

    
    {#each features as feature}
        <tr>
            <th><span>{feature.page}</span></th>
            <th><span style="color: var(--err-color)">{feature.missing_alts}</span></th>
            <th><span>{feature.meta_tags}</span></th>
            <th><span style="color: var(--err-color)">{feature.excess_bytes}</span></th>


            <th><Button msg="Optimize - $10" bcolor={"var(--active-color)"}/></th>
            <th><Button msg="Open" bcolor={"blue"} tcolor="white"/></th>
        </tr>
    {/each}
    
</table>



<style>

table, th {
  /*border:1px solid black;*/
  padding: 10px;
}

table {
    /*border:1px solid black;*/
    border-radius: 10px;
    box-shadow: 0px 0px 15px lightgray;
}

</style>