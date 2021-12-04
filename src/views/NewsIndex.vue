<template>
  <div class="news">
    <a href="https://github.com/login/oauth/authorize?client_id=b860c84ea950731da4f0">Sign into GitHub</a>
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
  //     var code = this.$route.query.code;
  //     if (code) {
  //       axios.get("/auth/github/callback?code=" + code).then((response) => {
  //         localStorage.setItem("github_access_token", response.data.access_token);
  //         this.$router.push("/about");
  //       });
  //     }
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