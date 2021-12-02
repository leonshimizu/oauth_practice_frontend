<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <ul>
      <li v-for="todo in todos">
        <p>ID: {{ todo.id }}</p>
        <p>Title: {{ todo.title }}</p>
        <button v-on:click="todoModal(todo)">Show More Info</button>
      </li>
    </ul>
    <dialog id="show-modal">
      <form method="dialog">
        <p>User ID: {{ currentTodo.userID }} </p>
        <p>ID: {{ currentTodo.id }} </p>
        <p>Title: {{ currentTodo.title }} </p>
        <p>Completed: {{ currentTodo.completed }} </p>
        <button>Close</button>
      </form>
    </dialog>
  </div>
</template>

<style></style>

<script>
  import axios from 'axios'
  export default {
    data: function () {
      return {
        message: "Welcome to Vue.js!",
        todos: [],
        currentTodo: {}
      };
    },
    created: function () {
      this.indexFunction();
    },
    methods: {
      indexFunction: function() {
        console.log("in the index function");
        axios 
          .get('https://jsonplaceholder.typicode.com/todos')
          .then(response => {
            console.log(response.data);
            this.todos = response.data;
          })
      },
      todoModal: function(theTodo) {
        console.log("in the show modal function");
        document.querySelector("#show-modal").showModal();
        this.currentTodo = theTodo;
      }
    },
  };
</script>