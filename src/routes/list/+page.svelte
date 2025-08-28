<script>
	let todos = $state([
		{ date: '2025/08/25', eventName: 'bday party' },
		{ date: '2025/08/27', eventName: 'soccer practice' },
		{ date: '2025/08/29', eventName: 'LAN party' }
	]);
	let newTodoText = $state('');
	let newTodoDate = $state('');

	function handleAdd() {
		if (newTodoText.length > 0) {
			const todoItem = {
				date: newTodoDate,
				eventName: newTodoText
			};
			todos.push(todoItem);
			newTodoText = '';
		}
	}
</script>

<div>
	<h1>Todo List ({todos.length})</h1>

	<input placeholder="todo name" bind:value={newTodoText} />
	<input bind:value={newTodoDate} type="date" />
	<button onclick={handleAdd}>add</button>
    <div id="listboxes">
        <div></div>
        <div></div>
        <div></div>
        <div></div>
        <div></div>
        <div></div>
        <div></div>
    </div>
    <!--
	<ol>
		{#each todos as v}
			<li>{v.date} - {v.eventName}</li>
		{/each}
	</ol>-->
</div>

<style>
#listboxes {
    display: grid;
    grid-template-rows: 7;
    min-height: 65vh;
    margin: 20px;
}
#listboxes > div {
    border: 1px solid grey;
}
</style>
