<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <ul>
      <li v-for="todo in todos">
        {{ todo }}
      </li>
    </ul>
  </div>
</template>

<style></style>

<script>
  import axios from 'axios'
  export default {
    data: function () {
      return {
        message: "Welcome to Vue.js!",
        todos: []
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
      }
    },
  };
</script>