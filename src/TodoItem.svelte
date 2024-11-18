<script>
  import { createEventDispatcher } from 'svelte';
  export let todo;

  const dispatch = createEventDispatcher();

  function handleDelete() {
    dispatch('delete', todo.id); // 'delete' 이벤트 전송
  }

  function handleToggle() {
    dispatch('toggle', todo.id); // 'toggle' 이벤트 전송
  }
</script>

<li>
  <span
    class:completed={todo.completed}
    on:click={handleToggle}
  >
    {todo.text}
  </span>
  <button on:click={handleDelete}>Delete</button>
</li>

<style>
  li {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin: 10px 0;
  }

  span {
    flex: 1;
    text-align: left;
    cursor: pointer;
  }

  span.completed {
    text-decoration: line-through;
    color: gray;
  }

  button {
    padding: 5px 10px;
    font-size: 14px;
    background-color: #e74c3c;
    color: white;
    border: none;
    cursor: pointer;
  }

  button:hover {
    background-color: #c0392b;
  }
</style>
