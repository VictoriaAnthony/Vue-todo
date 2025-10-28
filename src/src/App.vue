<template>
  <div style="max-width: 400px; margin: 2rem auto; font-family: sans-serif;">
    <h1>Vue Todo</h1>
    <TodoList />
  </div>
</template>

<script lang="ts">
import TodoList from "./components/TodoList.vue";

export default {
  components: { TodoList }
};
</script>
