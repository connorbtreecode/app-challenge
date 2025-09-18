<script>
	import { onMount } from "svelte";


	let todos = $state([]);
	let uniqueDates = $derived(getUniqueDates(todos));

	onMount(() => {
		if(localStorage.getItem("todos")) {
			todos = JSON.parse(localStorage.getItem("todos"));
		}
	})


	function getUniqueDates(todos) {
		let u = [];
		for(let t of todos) {
			if(!u.includes(t.date)) {
				u.push(t.date);
			}
		}
		u.sort();
		return u;
	}

	let newTodoText = $state('');
	let newTodoDate = $state('');

	function handleAdd() {
		if (newTodoText.length > 0 && newTodoDate.length > 0) {
			const todoItem = {
				date: newTodoDate,
				eventName: newTodoText
			};
			todos.push(todoItem);
			localStorage.setItem("todos", JSON.stringify(todos));
			newTodoText = '';
			newTodoDate = '';
		}
	}

	function handleDelete(index) {
		todos.splice(index, 1);
		localStorage.setItem("todos", JSON.stringify(todos))
	}
	
	const days = ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday', 'Sunday'];
	const months = [31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31]
	const monthNames = ["Janurary", "Feburary", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"]
</script>

<div>
	<h1>Todo List ({todos.length})</h1>

	<input placeholder="todo name" bind:value={newTodoText} />
	<input bind:value={newTodoDate} type="date" />
	<button onclick={handleAdd}>add</button>
	<div id="listboxes" style="margin-top: 7px;">
	{#each uniqueDates as d, index}
	<div>
		<div>{d}</div>
		<div>
			{#each todos.filter(v => v.date === d) as v, i}
				<div>
					{v.eventName}
					<button onclick={() => handleDelete(index)}>x</button>
				</div>
			{/each}
		</div>
	</div>
	{/each}
	</div>
	<!--<div id="listboxes">
		{#each todos as v, i}
			<div>{v.date}</div>
			<div>
				{v.eventName}
				<button onclick={() => handleDelete(i)}>x</button>
			</div>
		{/each}-
	</div>-->
</div>

<style>
	#listboxes {
		display: grid;
		grid-template-columns: 1fr;
		gap: 3px;
		min-height: 7vh;
	}
	#listboxes > * {
		background-color: lightgrey;
		padding: 4px;
		border: 1px solid grey;
	}
	*{font-family: "Space Mono", monospace; }
</style>
