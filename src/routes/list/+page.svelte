<script>
  let todos = $state([]);
  let newTodoText = $state("");

  $effect(function() {
    let savedData = localStorage.getItem("todo-list")
    todos = savedData.split(",");
  })

  function handleAdd() {
    if (newTodoText.length > 0) {
      todos.push(newTodoText);
      newTodoText = "";
      saveToLocalStorage();
    }
  }

  function saveToLocalStorage() {
    localStorage.setItem("todo-list", todos);
  }
</script>

<div>
  <h1>Todo List ({todos.length})</h1>

  <input bind:value="{newTodoText}" />
  <button onclick="{handleAdd}">add</button>

  <ol>
    {#each todos as v}
    <li>{v}</li>
    {/each}
  </ol>
</div>

<style></style>
