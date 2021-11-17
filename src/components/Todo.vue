<template>
  <div v-bind:class="{ completed: todo.completed }">
    <p v-on:click="markComplete">{{ todo.title }}</p>
    <button class="complete" @click="$emit('delete-todo', todo.id)">
      Delete
    </button>
    <button class="Edit" @click="$emit('edit-todo', todo.id)">Edit Task</button>
  </div>
</template>
<script>
export default {
  name: "Todo",
  props: ["todo"],
  methods: {
    markComplete() {
      this.todo.completed = !this.todo.completed;
      console.log("This is mark Complete in Todo.vue");
      var axios = require("axios");
      var data = "";
      var status = "";
      var idres = "";
      var id = this.todo.id;
      var config = {
        method: "get",
        url: "https://localhost:5001/api/Todo/" + id,
        withCredentials: false,
        headers: {
          Accept: "application/json",
          "Content-Type": "application/json",
        },
      };
      console.log(config);
      axios(config)
        .then(function (response) {
          console.log(JSON.stringify(response.data));
          status = response.data.completed;
          idres = response.data.id;
          if (status) {
            response.data.completed = false;
            data = JSON.stringify(response.data);
          } else {
            response.data.completed = true;
            data = JSON.stringify(response.data);
          }
          var url = "https://localhost:5001/api/Todo?id=" + idres;
          var config = {
            method: "put",
            url: url,
            headers: {
              "Content-Type": "application/json",
            },
            data: data,
          };

          axios(config)
            .then(function (response) {
              console.log(JSON.stringify(response.data));
            })
            .catch(function (error) {
              console.log(error);
            });
        })
        .catch(function (error) {
          console.log(error);
        });
    },
  },
};
</script>
<style scoped>
.completed {
  text-decoration: line-through;
}
.completed:hover {
  cursor: pointer;
}
</style>