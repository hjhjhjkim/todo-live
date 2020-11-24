<script>
  import { todoStore } from "../store.js";
  import Todo from "./todo.svelte";
  let todoInput;
  const max = (array) => {
    let maxValue = 0;
    array.forEach((todo) => {
      if (todo.id > maxValue) {
        maxValue = todo.id;
      }
    });
    return maxValue;
  };

  const addTodo = () => {
    todoStore.update((todoList) => {
      todoList.push({
        id: max(todoList) + 1,
        name: todoInput,
        created: Date.now(),
        checked: false,
      });
      return todoList;
    });
  };
</script>

<style lang="scss">
  @import "../scss/_definition.scss";
  .container {
    width: 100%;
    min-height: 100%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    .todo-wrapper {
      width: 600px;
    }
  }
</style>

<div class="container">
  <div class="todo-header">
    <input type="text" bind:value={todoInput} />
    <button on:click={addTodo}>추가</button>
  </div>
  <div class="todo-wrapper">
    {#each $todoStore as todo}
      <Todo {todo} />
      <!--><div class="box" />
      <p>{todo.name}</p>

      <div class="button" /><!-->
    {/each}
  </div>
</div>
