<script>

import authHeader from "@/services/auth-header";
import moment from 'moment'
export default {
  name: "Postlist",
  data() {
    return {
      posts: [],
      userInfos: {},
    }
  },
  methods: {
    async getPosts() {
      try {
// GET
        let response = await fetch("/api/post/allProfile", {
          headers: authHeader()
        });
        this.posts = await response.json();

      } catch (error) {
        console.log("Error", error);
      }
    },
    async getUserInfos() {
      // Fetch or Axios
      try {
        // Fetch returns a promise ( asynchronous)
        let response = await fetch("/api/userinfo/", {
          headers: authHeader()
        });
        this.userInfos = await response.json();
      } catch (error) {
        console.log("Error=", error);
      }
    },
  },
  created() {
    this.getPosts()
  }
}
</script>

<template>
  <div>
  <h1>List of Posts</h1>
  <ul>
    <li v-for="post in posts" :key="post.id">
      <h3> Book title: {{ post.book.title}} </h3>
      <h5> Post content: {{ post.content }} </h5>
      <h6> Post author: {{post.userInfo.firstName}} {{post.userInfo.lastName}}</h6>
      <br>
    </li>
  </ul>
    </div>


  </template>

  <style>
    .box {
      margin-bottom: 1rem;
    }
  </style>