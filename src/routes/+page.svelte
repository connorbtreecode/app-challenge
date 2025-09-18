<script>
	import { onMount } from "svelte";


	let todos = $state([]);
	let month = $state(new Date().getMonth());

	function getFirstDays() {
		let d = new Date();
		d.setMonth(month);
		d.setDate(1);
		let days = d.getDay();
		// 0 sunday - 6
		// 1 monday - 0
		// 2 tuesday - 1
		// 3 wedenesday - 2
		// 4 thursday - 3
		// 5 friday - 4
		// 6 saturday - 5
		days--;

		if(days < 0) {
			days = 6;
		}
		return new Array(days);
	}

	onMount(() => {
		if(localStorage.getItem("todos")) {
			todos = JSON.parse(localStorage.getItem("todos"));
		}
	})
	let days = ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday', 'Sunday'];
	const months = [31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31]
	const monthNames = ["Janurary", "Feburary", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"]
</script>

<div style="height: calc(100vh - 55px); display: flex; flex-direction: column;">
	<!-- calendar -->
	<div class="month">{monthNames[month]}</div>
	<div class="calendar">
		{#each days as day}
			<div style="display: flex; justify-content: center;">{day}</div>
		{/each}
		{#each getFirstDays() as day}
			<div style="display: flex; justify-content: center;"></div>
		{/each}
		{#each new Array(months[month]).fill(0) as day, i}
			<div>
				{i + 1}
				{#each todos.filter((v) => v.date.split('-')[2] == i + 1 && v.date.split('-')[1] - 1 == month) as v, i}
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
		display: flex;
		flex-wrap: wrap;
		flex-grow: 1;
	}
	
	.calendar > div {
		margin: 1px;
		background-color: skyblue;
		width: calc((100% - 14px) / 7);
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
