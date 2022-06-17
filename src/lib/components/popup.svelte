<script>
    import Button from '$lib/components/Button.svelte';

    
</script>

<body>




    <div id="popup">
        <slot></slot>


        <br/>
        <Button msg="Cancel" onclick="depop()"/>
    </div>
    
<script>
    function pop(){
        document.getElementById("popup").style.display="block";
    }

    function depop(){
        document.getElementById("popup").style.display="none";
    }
</script>
</body>
<style>

#popup {
    z-index: 10;
    box-shadow: 0 0 15px lightgray;
    border-radius: 15px;
    display: block;
    height: auto;
    width: auto;
    position: fixed;
    padding: 20px;
    background-color: white;

    /*center*/
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
}
</style>