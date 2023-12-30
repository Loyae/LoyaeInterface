<script>
    export let title = "box";
    export let id = "generated_meta_keywords";
    export let request = "meta()";
    export let topics = ["SEO", "AI"];
    

    
</script>


<!-- markup-->


<div class="card" id={id}>
    <div class="card-header">
    
<!--
    <section class="gauge">
    <div class="mask">
      <div class="semi-circle"></div>
      <div class="cover-degree" style="transform: rotate(80deg) translate3d(0, 0, 0);"></div>
    </div>
    </section>-->


     <div class="menu-dot"></div>
    </div>
    <div class="card-title" style="font-size: 1.2em;"><span style="color: lightcoral;"><div class="loader"></div> AI Generated</span> {title}</div>
    <div class="card-subtitle">
     
     <div class="output">
     <p><span style="color: #B0626B">&#x3C;meta</span> <span style="color: #4FA665">name=&#x22;<span style="color:#C76D43">keywords</span>&#x22; content=&#x22;</span></p>
      <textarea class="overflow-box" style="height:100px;">Generating...</textarea>
      <p style="color: #4FA665">&#x22;&gt;</p>
     </div>

    </div>
    <div class="detail-buttons">
        {#each topics as topic}
           <button class="search-buttons detail-button">{topic}</button>
        {/each}
    </div>
    <div class="card-buttons">
     <button class="shadow-hover search-buttons card-buttons" onclick="copyToClipboard(`generated_meta_keywords`)">Copy</button>
     <button class="shadow-hover search-buttons card-buttons-msg" onclick={request}>New</button>
    </div>
   </div>

   

<style>

  .card {
  padding: 20px 16px;
  background-color: var(--header-bg-color);
  border-radius: 8px;
  cursor: pointer;
  -webkit-transition: .2s;
  transition: .2s;
}

.card:hover {
  -webkit-transform: scale(1.02);
          transform: scale(1.02);
}

.card-header {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-align: start;
      -ms-flex-align: start;
          align-items: flex-start;
}

.card-title {
  font-weight: 600;
  margin-top: 16px;
  font-size: 14px;
}

.card-subtitle {
  color: var(--subtitle-color);
  font-size: 13px;
  margin-top: 14px;
  line-height: 1.6em;
}

.detail-button {
  background-color: var(--active-light-color);
  color: var(--active-color);
  font-size: 11px;
  font-weight: 500;
  padding: 6px 8px;
  border-radius: 4px;
}



.menu-dot {
  background-color: var(--placeholder-color);
  -webkit-box-shadow: -6px 0 0 0 var(--placeholder-color), 6px 0 0 0 var(--placeholder-color);
          box-shadow: -6px 0 0 0 var(--placeholder-color), 6px 0 0 0 var(--placeholder-color);
  width: 4px;
  height: 4px;
  border: 0;
  padding: 0;
  border-radius: 50%;
  margin-left: auto;
  margin-right: 8px;
}
</style>




