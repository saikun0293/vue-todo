<template>
  <div id="app">
    <AddTodo v-on:add-todo="addToDo" />
    <Todos v-bind:todos="todos" v-on:del-todo="deleteToDo" />
  </div>
</template>

<script>
import Todos from "../components/Todos";
import AddTodo from "../components/AddTodo";
import axios from "axios";

const url = "https://jsonplaceholder.typicode.com/todos";

export default {
  name: "Home",
  components: {
    Todos,
    AddTodo,
  },
  data() {
    return {
      todos: [
        {
          id: 1,
          title: "Don't believe in others!",
          completed: false,
        },
        {
          id: 2,
          title: "Don't make friends!",
          completed: false,
        },
        {
          id: 3,
          title: "Enjoy your own space",
          completed: false,
        },
      ],
    };
  },
  created() {
    axios
      .get(url + "?_limit=5")
      .then((res) => (this.todos = res.data))
      .catch((err) => console.log(err));
  },
  methods: {
    deleteToDo(id) {
      axios
        .delete(url + "/" + id)
        .then(() => {
          this.todos = this.todos.filter((t) => t.id != id);
        })
        .catch((err) => console.log(err));
    },
    addToDo(newTodo) {
      axios
        .post(url, newTodo)
        .then((res) => (this.todos = [...this.todos, res.data]))
        .catch((err) => console.log(err));
    },
  },
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.4;
}
.btn {
  background-color: #555;
  padding: 10px 20px;
  outline: none;
  border: none;
  font-weight: bolder;
  color: #fff;
  font-size: 15px;
}
</style>
