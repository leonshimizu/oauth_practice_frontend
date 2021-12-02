<template>
  <div class="news">
    <h1>{{ message }}</h1>
    <ul>
      <li v-for="post in posts.articles">
        {{ post }}
      </li>
    </ul>
  </div>
</template>

<style></style>

<script>
import axios from 'axios';
  export default {
    data: function () {
      return {
        message: "Welcome to the News!",
        posts: []
      };
    },
    created: function () {
      this.newsIndex();
    },
    methods: {
      newsIndex: function() {
        console.log("in the news index");
        axios
          .get('/news')
          .then(response => {
            console.log(response.data);
            this.posts = response.data;
          })
      }
    },
  };
</script>