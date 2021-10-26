<template>
  <div id="app">
    <Todos v-bind:todos="todos" v-on:delete-todo="deleteTodo" />
    <AddTodo v-on:add-todo="addTodo" />
  </div>
</template>
<script>
import axios from "axios";
import Todos from "./components/Todos";
import AddTodo from "./components/AddTodo";

export default {
  name: "app",
  components: {
    Todos,
    AddTodo,
  },
  data() {
    return {
      todos: [],
    };
  },
  created() {
    this.getData();
  },
  methods: {
    addTodo(newTodoObj) {
      this.todos = [...this.todos, newTodoObj];
      var axios = require("axios");
      var data = JSON.stringify({
        id: this.todos.length + 1,
        title: "newTodoObj",
        completed: true,
      });

      var config = {
        method: "post",
        url: "https://localhost:44368/api/Todo",
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
    },
    deleteTodo(todoId) {
      this.todos = this.todos.filter((todo) => todo.id !== todoId);
      var axios = require("axios");
      var data = "";

      var config = {
        method: "delete",
        url: "https://localhost:44368/api/Todo?id=" + todoId,
        headers: {},
        data: data,
      };

      axios(config)
        .then(function (response) {
          console.log(JSON.stringify(response.data));
        })
        .catch(function (error) {
          console.log(error);
        });
    },
    getData() {
      axios
        .get(
          "https://localhost:44368/api/Todo",
          {
            withCredentials: false,
            headers: {
              Accept: "application/json",
              "Content-Type": "application/json",
            },
          },
          {}
        )
        .then((todos) => {
          this.todos = todos.data;
        })
        .then(function (response) {
          console.log(response);
        })
        .catch(function (error) {
          console.log(" Error is: " + error);
        });
    },
  },
};
</script>
<style>
.complete {
  background-color: #4caf50; /* Green */
  border: none;
  color: white;
  padding: 5px 10px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
}
form {
  text-align: right;
}
h2 {
  text-align: center;
}
body {
  background: radial-gradient(circle, lightblue, white);
  font-family: "Noto Serif Armenian", "Noto Serif Georgian", "Noto Serif", serif;
  text-align: left;
}
ul,
li {
  margin: auto;
  width: 50%;
}
</style>