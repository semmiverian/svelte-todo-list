<script>
  export let newTodo;

  export let searchValue;

  let todoList = ["Bangun Tidur", "Mandi", "Gosok Gigi"];

  $: filteredTodo = todoList.filter(todo =>
    todo.match(new RegExp(searchValue, "i"))
  );

  $: {
    if (newTodo) {
      todoList = [...todoList, newTodo];
    }
  }

  let updateTodoIndex = null;

  let updateTodoText = "";

  function deleteTodo(deletedTodo) {
    const indexDeletedTodo = todoList.findIndex(todo => todo === deletedTodo);

    todoList = [
      ...todoList.slice(0, indexDeletedTodo),
      ...todoList.slice(indexDeletedTodo + 1, todoList.length)
    ];
  }

  function updateTodo(updatedTodo) {
    updateTodoIndex = todoList.findIndex(todo => todo === updatedTodo);
    updateTodoText = updatedTodo;
  }

  function submitUpdateTodo(e) {
    if (e.keyCode === 13) {
      const indexUpdateTodo = todoList.findIndex(
        (todo, index) => index === updateTodoIndex
      );

      todoList = [
        ...todoList.slice(0, indexUpdateTodo),
        updateTodoText,
        ...todoList.slice(indexUpdateTodo + 1, todoList.length)
      ];

      updateTodoIndex = null;
    }
  }
</script>

{#each filteredTodo as todo, index}
  <div class="flex flex-row w-100 mb-2 py-1 justify-between items-center">
    {#if index === updateTodoIndex}
      <input
        class="bg-gray-100 focus:bg-white focus:border-gray-200 border p-2
        flex-grow rounded appearance-none focus:outline-none mr-2"
        placeholder="Tekan Enter untuk mengupdate todo"
        on:keyup={submitUpdateTodo}
        bind:value={updateTodoText} />
    {:else}
      <span class="leading-normal tracking-wide text-lg text-gray-800">
        {todo}
      </span>
    {/if}
    <div class="flex flex-row">
      <!-- SVG untuk edit -->
      <svg
        xmlns="http://www.w3.org/2000/svg"
        viewBox="0 0 24 24"
        class="icon-edit w-4 h-4 mr-2 fill-current text-gray-400
        hover:text-blue-500 cursor-pointer"
        on:click={e => updateTodo(todo)}>
        <path
          class="primary"
          d="M4 14a1 1 0 0 1 .3-.7l11-11a1 1 0 0 1 1.4 0l3 3a1 1 0 0 1 0 1.4l-11
          11a1 1 0 0 1-.7.3H5a1 1 0 0 1-1-1v-3z" />
        <rect width="20" height="2" x="2" y="20" class="secondary" rx="1" />
      </svg>

      <!-- SVG untuk delete -->
      <svg
        xmlns="http://www.w3.org/2000/svg"
        viewBox="0 0 24 24"
        class="icon-trash w-4 h-4 fill-current text-gray-400 hover:text-red-500
        cursor-pointer"
        on:click={e => deleteTodo(todo)}>
        <path
          class="primary"
          d="M5 5h14l-.89 15.12a2 2 0 0 1-2 1.88H7.9a2 2 0 0 1-2-1.88L5 5zm5 5a1
          1 0 0 0-1 1v6a1 1 0 0 0 2 0v-6a1 1 0 0 0-1-1zm4 0a1 1 0 0 0-1 1v6a1 1
          0 0 0 2 0v-6a1 1 0 0 0-1-1z" />
        <path
          class="secondary"
          d="M8.59 4l1.7-1.7A1 1 0 0 1 11 2h2a1 1 0 0 1 .7.3L15.42 4H19a1 1 0 0
          1 0 2H5a1 1 0 1 1 0-2h3.59z" />
      </svg>
    </div>
  </div>
{/each}
