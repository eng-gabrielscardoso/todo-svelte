<script lang="ts">
  import { onMount } from "svelte";

  let inputTarget: HTMLInputElement;
  let todoInput: string;

  onMount(() => inputTarget.focus());

  function addTodo(event): void {
    event.preventDefault();

    if (todoInput.length < 3) {
      errors = [...errors, "Too small input"];
    } else {
      todos = [
        ...todos,
        {
          text: todoInput,
          checked: false,
        },
      ];

      todoInput = "";
    }
  }

  function removeTodo(index): void {
    todos.splice(index, 1);
    todos = [...todos];
  }

  function removeError(index): void {
    errors.splice(index, 1);
    errors = [...errors];
  }

  $: todos = [];
  $: errors = [];
</script>

<section class={`${$$props.class}`}>
  <div class="flex flex-col gap-2">
    {#if errors.length > 0}
      {#each errors as error, index}
        <div
          class="flex justify-between items-center p-1 bg-red-400 text-white rounded-md"
        >
          <span>{error}</span>
          <button>
            <i
              class="fa fa-times text-white"
              aria-hidden="true"
              on:click={() => removeError(index)}
            />
          </button>
        </div>
      {/each}
    {/if}
    <div>
      <form
        on:submit={(event) => addTodo(event)}
        class="flex gap-2 justify-between items-center align-center"
      >
        <input
          class="w-full px-2 py-1 bg-gray-100 rounded-md"
          type="text"
          name="todoInput"
          id="todoInput"
          bind:this={inputTarget}
          bind:value={todoInput}
          placeholder="Add a new todo"
        />
        <button
          disabled={!todoInput}
          class={`p-1 bg-blue-600 text-white rounded-md cursor-pointer ${
            !todoInput ? "bg-gray-300" : ""
          }`}
          on:click={(event) => addTodo(event)}>Add</button
        >
      </form>
    </div>
    {#if todos.length > 0}
      <ul>
        {#each todos as todo, index}
          <li class="my-1 flex gap-2 justify-between items-center align-center">
            <div class="flex gap-2 w-full truncate overflow-hidden">
              <input
                type="checkbox"
                name=""
                id=""
                bind:checked={todo.checked}
              />
              <p class={`${todo.checked ? "line-through" : ""}`}>
                {index + 1} - {todo.text}
              </p>
            </div>
            <button
              class="px-2 bg-red-600 rounded-md"
              on:click={() => removeTodo(index)}
            >
              <i class="fa fa-trash text-white" aria-hidden="true" />
            </button>
          </li>
        {/each}
      </ul>
    {:else}
      <div class="text-center">
        <quote>
          <i>"Today is always a task..."</i>
        </quote>
      </div>
    {/if}
  </div>
</section>
