<script>
  import TodoItem from './TodoItem.svelte';

  let todos = [
    { id: 1, text: 'Learn Svelte', completed: false },
    { id: 2, text: 'Build a To-Do App', completed: false },
    { id: 3, text: 'Deploy to Production', completed: false },
  ];

  let newTodo = '';

  function addTodo() {
    if (newTodo.trim()) {
      todos = [
        ...todos,
        { id: todos.length + 1, text: newTodo, completed: false },
      ];
      newTodo = '';
    }
  }

  function deleteTodo(event) {
    todos = todos.filter(todo => todo.id !== event.detail); // event.detail에 ID가 있음
  }

  function toggleComplete(event) {
    todos = todos.map(todo =>
      todo.id === event.detail ? { ...todo, completed: !todo.completed } : todo
    );
  }
</script>

<main>
  <h1>To-Do List</h1>

  <input
    type="text"
    placeholder="Add a new task"
    bind:value={newTodo}
    on:keypress={(e) => e.key === 'Enter' && addTodo()}
  />
  <button on:click={addTodo}>Add</button>

  <ul>
    {#each todos as todo}
      <TodoItem
        {todo}
        on:delete={deleteTodo}
        on:toggle={toggleComplete}
      />
    {/each}
  </ul>
</main>

<style>
  main {
    width: 400px;
    margin: 50px auto;
    font-family: Arial, sans-serif;
    text-align: center;
  }

  input {
    padding: 8px;
    width: 70%;
    font-size: 16px;
  }

  button {
    padding: 8px 15px;
    margin-left: 5px;
    font-size: 16px;
  }

  ul {
    list-style: none;
    padding: 0;
    margin-top: 20px;
  }
</style>