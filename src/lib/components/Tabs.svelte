<script>


    export let tabs;

   
</script>


<main>



<div id="tab-body">


<!-- Tab links -->
<div class="tab">
   {#each tabs as tab, i}
   <!--REPLACE WITH <Button/>-->
        {#if i == 0}
            <button class="tablinks" onclick="openTab(event, '{tab.id}')" id="default-tab">{tab.title}</button>
        {:else}
            <button class="tablinks" onclick="openTab(event, '{tab.id}')" id="default-tab">{tab.title}</button>
        {/if}
    {/each}
  </div>
  
  <div id="slot">
    <slot></slot>
  </div>
  
</div>


<script>


    function openTab(evt, tab) {

        
      var i, tabcontent, tablinks;
    
      tabcontent = document.getElementsByClassName("tab-content");
      for (i = 0; i < tabcontent.length; i++) {
        tabcontent[i].style.display = "none";
      }
      tablinks = document.getElementsByClassName("tablinks");
      for (i = 0; i < tablinks.length; i++) {
        tablinks[i].className = tablinks[i].className.replace(" active", "");
      }
      document.getElementById(tab).style.display = "block";
      evt.currentTarget.className += " active";
    }

    document.getElementById("default-tab").click();
    
    </script>

</main>




<style>
#tab-body {
    padding: 10px;
    background-color: var(--light-active-color);
    border-radius: 10px;
    
    width: 630px;
    height: auto;
    display: block;
}


/* Style the tab */
.tab {
  overflow: hidden;
  border: 0;
  background-color: var(--light-active-color);
  margin: 5px;
}

/* Style the buttons that are used to open the tab content */
.tab button {
  background-color: var(--active-color);
  border-radius: 10px;
  margin: 5px;
  float: left;
  border: none;
  outline: none;
  cursor: pointer;
  padding: 14px 16px;
  transition: 0.3s;
}

/* Change background color of buttons on hover */
.tab button:hover {
  background-color: #ddd;
}

/* Create an active/current tablink class */
.tab button.active {
  background-color: #ccc;
}

/*From other page*/
.tab-content {
  display: none;
  padding: 6px 12px;
  border: 1px solid #ccc;
  border-top: none;
}



</style>