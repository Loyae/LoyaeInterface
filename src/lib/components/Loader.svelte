<script>

</script>


<style>
.loader {
  border: 6px solid #f3f3f3;
  border-radius: 50%;
  border-top: 6px solid lightcoral;
  width: 20px;
  height: 20px;
  -webkit-animation: spin .8s linear infinite;
  /* Safari */
  animation: spin .8s linear infinite;
  display: block;
  float: left;
  margin-left: auto;
  margin-right: 10px;
}

/* Safari */
@-webkit-keyframes spin {
  0% {
    -webkit-transform: rotate(0deg);
  }
  100% {
    -webkit-transform: rotate(360deg);
  }
}

@keyframes spin {
  0% {
    -webkit-transform: rotate(0deg);
            transform: rotate(0deg);
  }
  100% {
    -webkit-transform: rotate(360deg);
            transform: rotate(360deg);
  }
}


</style>