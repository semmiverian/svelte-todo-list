<script>
  import AddTodo from "./components/AddTodo.svelte";
  import TodoList from "./components/TodoList.svelte";

  export let name;

  let searchValue = "";

  let newTodo = "";

  function addNewTodo(e) {
    newTodo = e.detail.newTodo;
  }
</script>

<style>
  h1 {
    color: purple;
  }
</style>

<div
  class="min-h-screen bg-gray-100 flex flex-row justify-center items-start p-10">
  <div class="bg-white pt-3 rounded shadow-xl w-1/2">
    <div class="px-3 mb-2">
      <span class="tracking-wide leading-normal text-lg text-gray-800">
        Svelte Todo List
      </span>
    </div>

    <AddTodo on:onAddTodo={addNewTodo} />

    <div class="bg-gray-100 py-3 rounded-b">
      <div class="px-3 mb-2 flex flex-row justify-end">
        <div class="relative">
          <input
            class="bg-gray-100 focus:bg-white focus:border-gray-200 border p-1
            rounded appearance-none focus:outline-none pl-5 "
            bind:value={searchValue}
            placeholder="Cari todo list" />

          <span class="absolute inset-y-0 left-0 flex items-center pl-1">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              viewBox="0 0 24 24"
              class="icon-search w-4 h-4 fill-current text-gray-100
              focus:text-black">
              <circle cx="10" cy="10" r="7" class="primary" />
              <path
                class="secondary fill-current text-gray-400"
                d="M16.32 14.9l1.1 1.1c.4-.02.83.13 1.14.44l3 3a1.5 1.5 0 0
                1-2.12 2.12l-3-3a1.5 1.5 0 0 1-.44-1.14l-1.1-1.1a8 8 0 1 1
                1.41-1.41zM10 16a6 6 0 1 0 0-12 6 6 0 0 0 0 12z" />
            </svg>
          </span>
        </div>
      </div>

      <div class="px-3 flex flex-col">
        <TodoList {newTodo} {searchValue} />
      </div>
    </div>
  </div>
</div>
