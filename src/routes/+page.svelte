<script>
	import { onMount } from "svelte";


	let todos = $state([]);

	onMount(() => {
		if(localStorage.getItem("todos")) {
			todos = JSON.parse(localStorage.getItem("todos"));
		}
	})
	let days = ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday', 'Sunday'];
	
</script>

<div>
	<!-- calendar -->
	<div class="calendar">
		{#each days as day}
			<div>{day}</div>
		{/each}
		{#each new Array(31).fill(0) as day, i}
			<div>
				{i + 1}
				{#each todos.filter((v) => v.date.split('-')[2] == i + 1) as v, i}
					<div class="event">{v.eventName}</div>
				{/each}
			</div>
		{/each}
	</div>
</div>

<style>
	.calendar {
		display: grid;
		grid-template-columns: repeat(7, 1fr);
		grid-auto-rows: 60px;
		min-height: 100vh;
	}

	.calendar > div {
		background-color: skyblue;
		margin: 1px;
	}

	.event {
    	font-size: 8px;
    	background-color: purple;
    	color: white;
    	padding: 2px 5px;
    	border-radius: 5px;
    	margin: 0.5px;
  	}
</style>
