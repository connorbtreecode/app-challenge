<script>
	import { onMount } from "svelte";


	let todos = $state([]);
	let month = $state(new Date().getMonth());

	onMount(() => {
		if(localStorage.getItem("todos")) {
			todos = JSON.parse(localStorage.getItem("todos"));
		}
	})
	let days = ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday', 'Sunday'];
	const months = [31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31]
	const monthNames = ["Janurary", "Feburary", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"]
	
</script>

<div>
	<!-- calendar -->
	<div class="month">{monthNames[month]}</div>
	<div class="calendar">
		{#each days as day}
			<div style="display: flex; justify-content: center;">{day}</div>
		{/each}
		{#each new Array(months[month]).fill(0) as day, i}
			<div>
				{i + 1}
				{#each todos.filter((v) => v.date.split('-')[2] == i + 1) as v, i}
					<div class="event">{v.eventName}</div>
				{/each}
			</div>
		{/each}
	</div>
	<div id="monthbuttons">
		<button onclick={() => {
			if(month == 0)
				month = 11
			else
				month -= 1
		}}>&lt;</button>
		<button onclick={() => {
			if(month == 11)
				month = 0
			else
				month += 1
		}}>&gt;</button>
	</div>
</div>

<style>
	.calendar {
		display: grid;
		grid-template-columns: repeat(7, 1fr);
		grid-template-rows: repeat(6, 1fr);
		height: 77vh;
	}

	.calendar > div {
		background-color: skyblue;
		margin: 1px;
	}

	.event {
    	font-size: 15px;
    	background-color: rgb(88, 146, 212); 	
		color: white;
    	padding: 2px 5px;
    	border-radius: 5px;
    	margin: 0.5px;
  	}
	#monthbuttons {
		display: flex; justify-content: space-around;
	}
	#monthbuttons * {
		font-size: 2em;
		border: 0px;
		background-color: white;
	}
	.month {
		font-size: 2em;
		display: flex;
		justify-content: center;
		margin: 7px;
	}
	*{font-family: "Space Mono", monospace; }
</style>
