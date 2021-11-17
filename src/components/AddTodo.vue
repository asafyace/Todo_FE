<template>
  <div>
    <form @submit="addTodo">
      <input type="text" v-model="title" name="title" />
      <button type="submit">Add</button>
    </form>
  </div>
</template>
<script>
import uuid from "uuid";
export default {
  name: "AddTodo",
  data() {
    return {
      title: "",
      idCount: 1,
    };
  },
  methods: {
    addTodo(e) {
      console.log("This is add in AddTodo.vue");
      e.preventDefault();
      const newTodoObj = {
        id: this.idCount,
        title: this.title,
        completed: false,
      };
      this.$emit("add-todo", newTodoObj);
      this.title = "";
      this.idCount++;
    },
  },
};
</script>
<style scoped>
</style>