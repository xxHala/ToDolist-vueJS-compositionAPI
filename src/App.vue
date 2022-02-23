<template>
  <div class="wrapper">
    <form @submit.prevent="addNewTodo">
      <h1>Add New Todo</h1>
      <div class="new-todo">
        <input v-model="newTodo" name="newTodo" />
        <button class="addButton">Add New Todo</button>
      </div>
      <div class="todos">
        <ul>
          <li v-for="(todo, index) in todos" :key="todo.id" class="todo">
            <h3 :class="{ done: todo.done }" @click="toggleDone(todo)">
              {{ todo.content }}
            </h3>
            <button @click="removeTodo(index)">Remove Todo</button>
          </li>
        </ul>
      </div>
    </form>
    <div class="buttons">
      <button class="remove" @click="removeAllTodos">Remove All</button>
      <button class="doneButton" @click="markAllDone">Mark All Done</button>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";

export default {
  setup() {
    const newTodo = ref("");
    const todos = ref([]);

    function addNewTodo() {
      todos.value.push({
        id: Date.now(),
        done: false,
        content: newTodo.value,
      });
      newTodo.value = "";
    }

    function toggleDone(todo) {
      todo.done = !todo.done;
    }

    function removeTodo(index) {
      todos.value.splice(index, 1);
    }

    function markAllDone() {
      todos.value.forEach((todo) => (todo.done = true));
    }

    function removeAllTodos() {
      todos.value.length = 0;
    }

    return {
      todos,
      newTodo,
      addNewTodo,
      toggleDone,
      removeTodo,
      markAllDone,
      removeAllTodos,
    };
  },
};
</script>

<style>
body {
  padding-top: 1em;
  padding-bottom: 1em;
  color: azure;
  font-size: 2em;
  background-image: linear-gradient(120deg, #5f57d1, #c065c0);
  margin: 0 auto;
}
.todos {
  margin: -7px 26px -1px -7px;
}
input,
textarea {
  font-weight: bold;
  width: 300px;
  margin: 0 35px 20px;
  height: 35px;
  padding: 6px 15px;
  border-radius: 5px;
  outline: none;
  border: none;
  background: #f6f7f9;
  color: #748194;
  font-size: 14px;
}

.new-todo {
  display: flex;
  flex-direction: column;
}

.new-todo input {
  width: 400px;
}

h1 {
  text-align: center;
  font-size: 30px;
  color: black;
  margin: 40px 20px;
}

form {
  color: #f2f5fa;
  font-size: 20px;
}

button {
  font-weight: bold;
  width: 230px;
  margin: 0 35px 20px;
  height: 45px;
  padding: 6px 15px;
  border-radius: 5px;
  outline: none;
  border: none;
  background: #ee9ba3;
  color: white;
  font-size: 14px;
}

.wrapper,
form,
#app {
  margin: 0 auto;
  max-width: 800px;
  display: flex;
  flex-direction: column;
}
.buttons {
  flex-direction: row;
  display: flex;
}
.buttons button {
  width: 50%;
  border-radius: 4px;
}
.addButton {
  background: rgb(49, 161, 143);
  align-self: end;
  width: 30% !important;
}

.remove {
  background: red;
}

.todo {
  cursor: pointer;
  display: flex;
  justify-content: space-between;
}

.done {
  text-decoration: line-through;
}

li {
  background: #f2f5fa;
  color: black;
  list-style: none;
  font-size: 20px;
  border-radius: 6px;
  margin: 10px;
}

ul button {
  width: 27%;
  align-self: flex-end;
  margin: 12px;
}
</style>
