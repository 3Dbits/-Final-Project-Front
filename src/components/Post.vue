<template>
  <header>
    <h3>{{ content }}</h3>
  </header>
</template>
<script></script>
  <script>
  import authHeader from "@/services/auth-header";
  export default {

    data() {
      return {
        posts: [],
        urlAddOn: "?bookName=",
        name: "Search",
      };
    },
    methods: {
      async getPosts() {
        // Fetch or Axios
        try {
          // Fetch returns a promise ( asynchronous)
          let response = await fetch("http://localhost:8080/api/post" + this.urlAddOn + this.name, {
            headers: authHeader()
          });
          this.posts = await response.json();
        } catch (error) {
          console.log("Error=", error);
        }
      }
    }
  }
  </script>
  <style>
  </style>