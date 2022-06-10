<script>
    export let title;

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

        

        <tr class="odd">
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
        </tr>
       
    </tbody>

</table>



<style>
    
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

table.timecard thead th #thDay {
	width: 40%;	
}

table.timecard thead th #thRegular, table.timecard thead th#thOvertime, table.timecard thead th#thTotal {
	width: 20%;
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