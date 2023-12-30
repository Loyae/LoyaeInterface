<script>
  import { dataset_dev } from "svelte/internal";


    export let title;
    export let data;
    export let ths;
</script>


<table class="timecard">
    <caption>{title}</caption>
    <thead>
        <tr>
            {#each ths as th}
            <th>{th}</th>
            {/each}
        </tr>
    </thead>
    <tbody>
        <!-- {i%2==0 ? 'even' : 'odd'} -->
        <!-- <p>{data[0].page}</p> -->
         {#each Array(data.length) as _, i}
        <tr class="{i%2==0 ? 'even' : 'odd'}">
            <th>▶</th>
            <th>{data[i].Whois.title}</th>
            <td>{data[i].Whois.domain}</td>
            <td>{data[i].FetchMeta.description}</td>
            <td>{data[i].MissingAlts}</td>
        </tr>
        
        {/each} 

        <!-- <tr class="odd">
            <th>Monday</th>
            <td>8</td>
            <td>0</td>
            <td>8</td>
        </tr>
        <tr class="even">
            <th>Tuesday</th>
            <td>8</td>
            <td>2.5</td>
            <td>10.5</td>
        </tr> -->
        
       
    </tbody>

</table>



<style>
/*
table tr:last-child td:first-child {
    border: 2px solid red;
    border-bottom-left-radius: 10px;
    }
    
table tr:last-child td:last-child {
    border: 2px solid green;
    border-bottom-right-radius: 10px;
}*/

caption {
    border-top-right-radius: 10px;
    border-top-left-radius: 10px;
    padding: 5px;
}
    
table.timecard {
	margin: auto;
	width: 600px;
	border-collapse: collapse;
	box-shadow: 0 0 15px lightgray;
}

table.timecard caption {
	background-color: var(--active-color);
	color: #fff;
	letter-spacing: .3em;
}

table.timecard thead th {
	padding: 8px;
	background-color: white;
	font-size: large;
}



table.timecard th, table.timecard td {
	padding: 3px;
	border-width: 1px;
	border-style: solid;
	border-color: var(--light-active-color) lightgray;
}

table.timecard td {
	text-align: right;
}

table.timecard tbody th {
	text-align: left;
	font-weight: normal;
}

table.timecard tr.even {
	background-color: var(--light-active-color);
}
table.timecard tr.odd {
	background-color: white;
}
</style>