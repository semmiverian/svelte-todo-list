<script>
  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();

  let newTodo = "";

  function addNewTodo(e) {
    dispatch("onAddTodo", { newTodo });
    newTodo = "";
  }
</script>

<form on:submit|preventDefault={addNewTodo}>
  <div class="px-3 flex flex-row pb-4 mb-2">
    <div class="relative flex-grow flex text-gray-400">

      <input
        class="bg-gray-100 focus:bg-white focus:border-gray-200 border p-2
        flex-grow mr-2 rounded appearance-none focus:outline-none pl-5
        text-black"
        placeholder="Masukan todo list baru"
        bind:value={newTodo} />
      <span class="absolute inset-y-0 left-0 flex items-center">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          viewBox="0 0 24 24"
          class="icon-add w-6 h-6 fill-current">
          <path
            class="secondary"
            fill-rule="evenodd"
            d="M17 11a1 1 0 0 1 0 2h-4v4a1 1 0 0 1-2 0v-4H7a1 1 0 0 1 0-2h4V7a1
            1 0 0 1 2 0v4h4z" />
        </svg>
      </span>
    </div>

    <button
      class="text-lg bg-blue-500 p-2 rounded shadow-lg text-white"
      type="submit">
      Tambah Todo
    </button>
  </div>
</form>
