<script>
	import { onMount } from "svelte";


	let todos = $state([]);

	onMount(() => {
		if(localStorage.getItem("todos")) {
			todos = JSON.parse(localStorage.getItem("todos"));
		}
	})

	let newTodoText = $state('');
	let newTodoDate = $state('');
	let keyNumber = 0; 
	// function setLocalStorageItem(eventObj) {
	// 	// if(localStorage.getItem("keyCount") !== null) {
	// 		// keyNumber = localStorage.getItem("keyCount");
	// 	// }
	// 	let objAr = { date: eventObj.date, eventName: eventObj.eventName };
	// 	// localStorage.setItem(keyNumber, JSON.stringify(objAr));
	// 	// keyNumber++;
	// 	// localStorage.setItem("keyCount", keyNumber);
	// 	todos.push(objAr);
	// 	localStorage.setItem("todos", JSON.stringify(todos));
	// }
	function handleAdd() {
		if (newTodoText.length > 0 && newTodoDate.length > 0) {
			const todoItem = {
				date: newTodoDate,
				eventName: newTodoText
			};
			// setLocalStorageItem(todoItem)
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
</script>

<div>
	<h1>Todo List ({todos.length})</h1>

	<input placeholder="todo name" bind:value={newTodoText} />
	<input bind:value={newTodoDate} type="date" />
	<button onclick={handleAdd}>add</button>
	<div id="listboxes">
		{#each todos as v, i}
			<div>{v.date}</div>
			<div>
				{v.eventName}
				<button onclick={() => handleDelete(i)}>x</button>
			</div>
		{/each}
	</div>
</div>

<style>
	#listboxes {
		display: grid;
		grid-template-columns: auto 1fr;
		gap: 3px;
	}
	#listboxes > div {
		background-color: #eee;
		padding: 4px;
	}
</style>
