<template>
  <div>
    <h2>My To Do List</h2>
    <ul>
      <li v-bind:key="todo.id" v-for="todo in todos">
        <Todo
          v-bind:todo="todo"
          v-on:delete-todo="$emit('delete-todo', todo.id)"
          v-on:edit-todo="$emit('edit-todo', todo.id)"
        />
      </li>
    </ul>
  </div>
</template>
<script>
import Todo from "./Todo";
export default {
  name: "Todos",
  components: {
    Todo,
  },
  props: ["todos"],
  methods: {},
};
</script>
<style scoped>
</style>