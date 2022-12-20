<script>

import authHeader from "@/services/auth-header";
import moment from 'moment'
export default {
  name: "Postlist",
  data() {
    return {
      posts:{},
    }
  },
  methods: {
    async getPosts() {
      try {
// GET
        let response = await fetch("http://localhost:8080/api/post/", {
          headers: authHeader()
        });
        this.posts = await response.json();

      } catch (error) {
        console.log("Error", error);
      }
    }
  }
}
</script>

<template>
  <div>
    <h3 class="title">Recent Posts</h3>

    <div v-for="post in posts" :key="post.id" class="box">

      <h2 class="subtitle">{{ post.creation_date }}</h2>

      <p>{{ post.content }}</p>
    </div>
  </div>
  </template>

  <style>
    .box {
      margin-bottom: 1rem;
    }
  </style>