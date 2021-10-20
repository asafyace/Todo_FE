<template>
  <div v-bind:class="{ completed: todo.completed }">
    <p v-on:click="markComplete">{{ todo.title }}</p>
    <button class="complete" @click="$emit('delete-todo', todo.id)">
      Completed
    </button>
  </div>
</template>
<script>
export default {
  name: "Todo",
  props: ["todo"],
  methods: {
    markComplete() {
      this.todo.completed = !this.todo.completed;
    },
  },
};
</script>
<style scoped>
.completed {
  text-decoration: line-through;
}
</style>