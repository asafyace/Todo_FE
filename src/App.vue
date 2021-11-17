<template>
  <div id="app">
    <Todos
      v-bind:todos="todos"
      v-on:delete-todo="deleteTodo"
      v-on:edit-todo="editTodo"
    />
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
      idCount: 1,
    };
  },
  created() {
    this.getData();
  },
  methods: {
    getData() {
      axios
        .get(
          "https://localhost:5001/api/Todo",
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
    addTodo(newTodoObj) {
      console.log("This is Add in app vue");
      this.todos = [...this.todos, newTodoObj];
      var axios = require("axios");
      var data = JSON.stringify({
        id: this.idCount,
        title: newTodoObj.title,
        completed: false,
      });
      var config = {
        method: "post",
        url: "https://localhost:5001/api/Todo",
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
      this.idCount++;
    },
    deleteTodo(todoId) {
      console.log("This is delete in app.vue");

      console.log("To do id from function call " + todoId);

      this.todos = this.todos.filter((todo) => todo.id !== todoId);
      var axios = require("axios");
      var data = "";
      var config = {
        method: "delete",
        url: "https://localhost:5001/api/Todo?id=" + todoId,
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
      //this.idCount++;
    },
    editTodo(todoId) {
      console.log("This is edit in app.vue");

      console.log("To do id from function call " + todoId);

      this.todos = this.todos.filter((todo) => todo.id !== todoId);
      var axios = require("axios");
      var data = "";
      var config = {
        method: "delete",
        url: "https://localhost:5001/api/Todo?id=" + todoId,
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
      //this.idCount++;
    },
  },
};
</script>
<style>
.complete {
  background-color: #f44336; /* red */
  border: none;
  color: white;
  padding: 5px 10px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
}
.complete:hover {
  font-size: 18px;
}
.Edit {
  background-color: greenyellow; /* red */
  border: none;
  color: white;
  padding: 5px 10px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
}
.Edit:hover {
  font-size: 18px;
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
  list-style-type: circle;
  margin: auto;
  width: 50%;
}
</style>