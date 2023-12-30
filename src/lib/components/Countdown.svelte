<script>
  export let date;

    		let countdown_days = 1;
					let countdown_hours = 1;
					let countdown_minutes = 1;
					let countdown_seconds = 1;
	   
	   function getTimeRemaining(endtime) {
		   const total = Date.parse(endtime) - Date.parse(new Date());
		   const seconds = Math.floor((total / 1000) % 60);
		   const minutes = Math.floor((total / 1000 / 60) % 60);
		   const hours = Math.floor((total / (1000 * 60 * 60)) % 24);
		   const days = Math.floor(total / (1000 * 60 * 60 * 24));
		   
		   return {
			 total,
			 days,
			 hours,
			 minutes,
			 seconds
		   };
		 }
		 
		 async function initializeClock(endtime) {
		 
		  function updateClock() {
			 const t = getTimeRemaining(endtime);
		 
			 countdown_days = t.days;
			 countdown_hours = ('0' + t.hours).slice(-2);
			 countdown_minutes = ('0' + t.minutes).slice(-2);
			 countdown_seconds = ('0' + t.seconds).slice(-2);
		 
			 if (t.total <= 0) {
			   clearInterval(timeinterval);
			 }
		   }
		 const timeinterval = setInterval(updateClock, 1000);
		   updateClock();
		   

		   
		 }
		 
		 const deadline = new Date(Date.parse(date)); //dec 9th 2023
		 initializeClock(deadline);
</script>

<b>{countdown_days} days : {countdown_hours} hours : {countdown_minutes} minutes : {countdown_seconds} seconds</b>