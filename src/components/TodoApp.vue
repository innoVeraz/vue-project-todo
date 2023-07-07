<script setup lang="ts">
import { ref } from "vue";
import { Todo } from "../models/Todo";
import TodoView from "./TodoView.vue";
import AddTodo from "./AddTodo.vue";

const todos = ref<Todo[]>([]);

//vid knapptryck blir todos.value en ny todo med egenskaperna user input (text) inte done och får ett id som är datum och tidpunkt
const addTodo = (text: string) => {
  todos.value = [...todos.value, new Todo(text, false, new Date().getTime())];
};

//vid klick på li loopa igenom todo.value med map, för varje todo, om todo.id är lika med
const toggleTodo = (id: number) => {
  todos.value = todos.value.map((todo) => {
    if (todo.id === id) {
      return { ...todo, done: !todo.done };
    } else {
      return todo;
    }
  });
};
</script>

<template>
  <AddTodo @addtodo="addTodo"></AddTodo>
  <div>
    <TodoView
      @toggle="toggleTodo"
      v-for="todo in todos"
      :key="todo.id"
      :todo="todo"
    >
    </TodoView>
  </div>
</template>

<style scoped>
ul {
  list-style-type: none;
  margin: 0;
  padding: 0;
}

.done {
  text-decoration: line-through;
}
</style>
