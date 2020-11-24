<script>
  import { todoStore } from "../store.js";
  export let todo;
  const toggleCheck = () => {
    $todoStore.forEach((t) => {
      if (t.id === todo.id) {
        t.checked = !t.checked; //반대값으로 바꿔줌.true면 false로.
      }
    });
    todoStore.set($todoStore);
  }; //const finded = $todoStore.filter((t) => t.id === todo.id)[0];
  //todo.id: 지정해준 고유값. filter 함수가 돌면서 t를 지정하고, 고유값과 비교.return값으로 트루인 애들만 골라서 array 만드는 게 filter.-->
  const deleteFunc = () => {
    console.log("delete", todo.id);
    todoStore.set($todoStore.filter((t) => !(t.id === todo.id)));
    //$todoStore = $todoStore.filter((t) => !(t.id === todo.id));filter로 todo.id가 아닌 애들 전부를 골라서 새 배열을 만듦.filter, max, return이 삼대장.
  };
</script>

<style lang="scss">
  @import "../scss/_definition.scss";
  .todo {
    width: 100%;
    border: 1px solid gray;
    margin-bottom: 16px;
  }
  .box {
    width: 16px;
    height: 16px;
    background-color: white;
    border: 1px solid red;
    &.true {
      background-color: red;
    }
  }
</style>

<div class="todo">
  <div class="box {todo.checked}" on:click={toggleCheck} />
  <div class="title">{todo.name}</div>
  <div class="created">{todo.created}</div>
  <button on:click={deleteFunc} class="delete-button">x</button>
</div>
