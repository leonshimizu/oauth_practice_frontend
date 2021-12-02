<template>
  <div class="news">
    <h1>{{ message }}</h1>
    <ul>
      <li v-for="post in posts.articles">
        <p>Author: {{ post.author }}</p>
        <p>Title: {{ post.title }}</p>
        <p>Content: {{ post.content }}</p>
        <button v-on:click="newsModal(post)">Show More Info</button>
      </li>
    </ul>
    <dialog id="news-modal">
      <form method="dialog">
        <p>Author: {{ currentPost.author }}</p>
        <p>Title: {{ currentPost.title }}</p>
        <p>Description: {{ currentPost.description }}</p>
        <p>URL: {{ currentPost.url }}</p>
        <p>Published At: {{ currentPost.publishedAt }}</p>
        <button>Close</button>
      </form>
    </dialog>
  </div>
</template>

<style></style>

<script>
import axios from 'axios';
  export default {
    data: function () {
      return {
        message: "Welcome to the News!",
        posts: [],
        currentPost: {}
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
      },
      newsModal: function(thePost) {
        console.log("in the news modal");
        document.querySelector("#news-modal").showModal();
        this.currentPost = thePost;
      }
    },
  };
</script>