<script>
    export let title;
    export let prompt;
    export let direct;
    export let APIURL;
    
    
	import Button from '$lib/components/Button.svelte';
</script>


<div id="form">
    <h3>{title}</h3>
    <div class="form-button">
        <Button bcolor={"#D84457"} tcolor={"white"} msg={"Google"} direct={APIURL + "/loginGoogle"} width="100%"/>
    </div>

    <div class="form-button">
        <Button bcolor={"black"} tcolor={"white"} msg={"Github"} direct={APIURL + "/loginGH"} width="100%"/>
    </div>

    <div class="form-button">
        <Button bcolor={"#0072B1"} tcolor={"white"} msg={"Linkedin"} direct="" width="100%"/>
     </div>

    <div class="form-button">
        <Button bcolor={"#1877F2"} tcolor={"white"} msg={"Facebook"} direct={APIURL + "/loginFB"} width="100%"/>
    </div>
    <br/>
    <hr/>
    <br/>


    <form method="post" action="{direct}">

        {#if title == "Sign Up"}
        <input type="text" id="username" name="username" placeholder="Username:"><br>
        {/if}

        <input type="text" id="email" name="email" placeholder="Email:"><br>

        <input type="password" id="password" name="password" placeholder="Password:"><br>

        {#if title == "Sign Up"}
            <input type="text" id="confirmpass" name="confirmpass" placeholder="Re-Type Password:"><br>
        {/if}
        
        <!--<input type="submit" value="SIGN IN"/>-->
        <div class="form-button">
            <Button bcolor={"var(--active-color)"} tcolor={"white"} msg={prompt} width="100%" type="submit"/>
        </div>
      </form> 

    

    <br/>

    {#if title == "Sign Up"}
        <span>Have an account? Log in <a href="/signin">here</a>!</span>
    {:else}
        {#if title == "Sign In"}
            <span>Don't have an account? Sign up <a href="/signup">here</a>!</span>
        {/if}
    {/if}




</div>


<style>
    #form {
        box-shadow: 0 0 15px lightgray;
        position: relative;
        justify-content: center;
        border-radius: 15px;
        padding: 10px;
        margin: 40px 10px 10px 10px;
        height: auto;
        width: 400px;
    }

    .form-button {
        margin: 10px;
    }

    input {
        display: block;
        padding: 10px;
        background-color: #fdf1f1;
        border-radius: 10px;
        width: 100%;
        height: 40px;
        border: 0;
    }

    input::placeholder {
        color: var(--active-color);
        font-weight: bold;
    }

</style>