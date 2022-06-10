<script>
    export let title;
    export let prompt;
    export let direct;
    
    
	import Button from '$lib/components/Button.svelte';
</script>


<div id="form">
    <h3>{title}</h3>
    <div class="form-button">
        <Button bcolor={"red"} tcolor={"white"} msg={"Google"} direct={direct} width="100%"/>
    </div>

    <div class="form-button">
        <Button bcolor={"black"} tcolor={"white"} msg={"Github"} direct={direct} width="100%"/>
    </div>

    <div class="form-button">
        <Button bcolor={"blue"} tcolor={"white"} msg={"Linkedin"} direct={direct} width="100%"/>
     </div>

    <div class="form-button">
        <Button bcolor={"blue"} tcolor={"white"} msg={"Facebook"} direct={direct} width="100%"/>
    </div>
    <br/>
    <hr/>
    <br/>


    <form action="/action_page.php">
        <label for="fname">First Name</label><br>
        <input type="text" id="fname" name="fname" value="John"><br>
        <label for="lname">Last Name:</label><br>
        <input type="text" id="lname" name="lname" value="Doe"><br>
        <label for="lname">Email:</label><br>
        <input type="text" id="lname" name="lname" value="Doe"><br>
        <label for="lname">Password:</label><br>
        <input type="text" id="lname" name="lname" value="Doe"><br>
        <label for="lname">Re-Type Password:</label><br>
        <input type="text" id="lname" name="lname" value="Doe"><br>
        <!--<input type="submit" value="Submit">-->
      </form> 

    <div class="form-button">
        <Button bcolor={"var(--active-color)"} tcolor={"white"} msg={prompt} direct={direct} width="100%"/>
    </div>



</div>


<style>
    #form {
        box-shadow: 0 0 15px lightgray;
        position: relative;
        justify-content: center;
        border-radius: 15px;
        padding: 10px;
        margin: 40px 10px 10px 10px;
        height: 600px;
        width: 400px;
    }

    .form-button {
        margin: 10px;
    }


</style>