<template>
  <div class="about">
    <h1>This is an about page</h1>
    {{ profile }}
  </div>
</template>

<script>
  import axios from "axios";

  export default {
    data: function() {
      return {
        profile: {}
      }
    },
    created: function () {
      var githubAccessToken = localStorage.getItem("github_access_token");
      if (githubAccessToken) {
        axios
          .get("/github_profile?github_access_token=" + githubAccessToken)
          .then((response) => {
            console.log(response.data);
            this.profile = response.data;
          });
      }
    },
  };
</script>