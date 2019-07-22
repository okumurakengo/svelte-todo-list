<script>
  import { afterUpdate } from "svelte";
  afterUpdate(() => {
    document.querySelector(".js-todo-input").focus();
  });

  let todoItems = [];
  let newTodo = "";

  function addTodo() {
    newTodo = newTodo.trim();
    if (!newTodo) return;

    todoItems = [...todoItems, { text: newTodo, complete: false }];
    newTodo = "";
  }

  function toggleDone(index) {
    todoItems[index].complete = !todoItems[index].complete;
  }

  function removeTodo(index) {
    todoItems = todoItems.filter((_, i) => i !== index);
  }

  let value = "world";
</script>

<style>
  h1 {
    color: purple;
  }

  .done {
    text-decoration: line-through;
  }

  .delete {
    color: #777;
    text-decoration: none;
  }
</style>

<h1>Hello {value} !</h1>
<form on:submit|preventDefault={addTodo}>
  <input type="text" class="js-todo-input" bind:value={newTodo} />
  <button type="submit">Add Todo</button>
</form>
<ul>
  {#each todoItems as todo, index}
    <li>
      <input
        id={index}
        type="checkbox"
        bind:checked={todo.complete}
        on:click={() => toggleDone(index)} />
      <span class={todo.complete ? 'done' : ''}>{todo.text}</span>
      <a
        href="#hoge"
        class="delete"
        on:click|preventDefault={() => removeTodo(index)}>
        [x]
      </a>
    </li>
  {/each}
</ul>
