<script>
export let hrefs;
export let logo_href;
export let title;
//export let active_href = 0;
</script>

<div class="header">
	   
    <a href="../index.html" style="text-decoration: none; color: black">
      <div class="logo">
         <img src={logo_href} alt="logo" height="30px" width="30px" style="margin: 3px;"/>
       {title}
      </div>
    </a>
    
      <div class="header-menu">
        {#each hrefs as href}
        <a href={href[1]}>{href[0]}</a>
      {/each}

      

      </div>
      <div class="user-settings">
       
       <div class="user-name">By John Lins</div>
      </div>
     </div>


<style>

.logo {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-align: center;
      -ms-flex-align: center;
          align-items: center;
  font-weight: 600;
  font-size: 18px;
  cursor: pointer;
}
	.header {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-align: center;
      -ms-flex-align: center;
          align-items: center;
  -webkit-transition: -webkit-box-shadow 0.3s;
  transition: -webkit-box-shadow 0.3s;
  transition: box-shadow 0.3s;
  transition: box-shadow 0.3s, -webkit-box-shadow 0.3s;
  -ms-flex-negative: 0;
      flex-shrink: 0;
  padding: 0 40px;
  white-space: nowrap;
  background-color: var(--header-bg-color);
  /*background-color: rgba(255, 255, 255, .01);
backdrop-filter: blur(5px);
-moz-filter: blur(15px);
  */
  height: 60px;
  width: 100%;
  font-size: 14px;
  -webkit-box-pack: justify;
      -ms-flex-pack: justify;
          justify-content: space-between;
}

.header-menu a {
  text-decoration: none;
  color: var(--body-color);
  font-weight: 500;
}

.header-menu a:hover {
  color: var(--active-color);
}

.header-menu a:not(:first-child) {
  margin-left: 30px;
}


@media screen and (max-width: 590px) {
  .header-menu {
    display: none;
  }
}


@media screen and (max-width: 760px) {
  .user-name {
    display: none;
  }
}
 
</style>