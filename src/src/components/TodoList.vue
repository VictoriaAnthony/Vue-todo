<template>
  <div>
    <input v-model="task" placeholder="Add task" />
    <button @click="addTodo">Add</button>
    <ul>
      <li v-for="todo in todos" :key="todo.id">
        <input type="checkbox" v-model="todo.completed" />
        {{ todo.task }}
        <button @click="deleteTodo(todo.id)">Delete</button>
      </li>
    </ul>
  </div>
</template>

<script lang="ts">
import { reactive, ref } from "vue";

type Todo = { id: number; task: string; completed: boolean };

export default {
  setup() {
    const task = ref("");
    const todos = reactive<Todo[]>(JSON.parse(localStorage.getItem("todos") || "[]"));

    const addTodo = () => {
      if (!task.value) return;
      todos.push({ id: Date.now(), task: task.value, completed: false });
      task.value = "";
      localStorage.setItem("todos", JSON.stringify(todos));
    };

    const deleteTodo = (id: number) => {
      const index = todos.findIndex(t => t.id === id);
      if (index > -1) todos.splice(index, 1);
      localStorage.setItem("todos", JSON.stringify(todos));
    };

    return { task, todos, addTodo, deleteTodo };
  }
};
</script>
