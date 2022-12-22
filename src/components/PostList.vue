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
    <br>
  <ul>
    <li v-for="post in posts" :key="post.id">
      <article class="media">
        <figure class="media-left">
          <p class="image is-64x64">
            <img :src=post.book.smallThumbnail>
          </p>
        </figure>
        <div class="media-content">
          <div class="content">
            <router-link :to="{name: 'PostPage', query: {id: post.id}}">
            <p>
              <small>{{post.userInfo.firstName}} {{post.userInfo.lastName}}</small>
              <br>
              <strong>{{post.book.title}}</strong>
              <br>
              {{ post.content }}
            </p>
            </router-link>
            <br>
          </div>
        </div>
      </article>
      <br>
    </li>
  </ul>
    <p v-if="posts.length === 0">You have not any post,
      <router-link to="/search">use this link to search books</router-link></p>
  </div>


  </template>

  <style>
    .box {
      margin-bottom: 1rem;
    }
  </style>