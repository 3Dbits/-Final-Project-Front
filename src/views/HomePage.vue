<template>

  <h1>All post by your friends:</h1>
  <br>
  <div v-for="post in posts" :key="post.id">
    <div class="box">
<!--      <div class="field">-->
<!--        <p>{{post.createAt}}</p>-->
<!--        <p>{{post.updateAt}}</p>-->
<!--        <p>{{post.content}}</p>-->
<!--        <p>{{post.book.title}}</p>-->
<!--        <p>{{post.userInfo.firstName}}</p>-->
<!--        <p>{{post.userInfo.lastName}}</p>-->
<!--      </div>-->
<!--    </div>-->
<!--    /////////////-->
      <router-link :to='"/post?id=" + post.id' >
    <article class="media">
      <div class="media-left">
        <figure class="image is-64x64">
          <img :src=post.book.smallThumbnail alt="bookcover" v-if='post.book.smallThumbnail !== "none"'>
        </figure>
      </div>
      <div class="media-content">
        <div class="content">
          <p>
            <strong>{{post.book.title}}</strong> by <strong v-for="author in post.book.authors">{{author.name}}</strong>
            <br>
            <small>{{post.userInfo.firstName}} {{post.userInfo.lastName}}</small> <small>at {{post.createAt.substr(0,10)}}</small>
            <br>
            {{post.content}}
          </p>
        </div>
        <nav class="level is-mobile">
          <div class="level-left">
            <a class="level-item" aria-label="like">
            <span class="icon is-small">
              <font-awesome-icon icon="fa-solid fa-hand-holding-heart" />
            </span>
            </a>
            <a class="level-item" aria-label="like">
            <span class="icon is-small">
              10
            </span>
            </a>
          </div>
        </nav>
      </div>
    </article>
      </router-link>
    </div>

  </div>
</template>

<script>
import authHeader from "@/services/auth-header";

export default {
  name: "HomePage",
  data() {

    return {
      posts: [],
    };
  },
  methods: {
    async getBooks() {
      // Fetch or Axios
      try {
        // Fetch returns a promise ( asynchronous)
        let response = await fetch("http://localhost:8080/api/post/all", {
          headers: authHeader()
        });
        this.posts = await response.json();
      } catch (error) {
        console.log("Error=", error);
      }
    },
  },
  created() {
    this.getBooks();
  }
}
</script>

<style scoped>
 .box {
   max-width: 80%;
   margin: auto;
   margin-bottom: 5px;
 }
 a:hover, a:active {
   text-decoration: none;
   color: inherit;
 }
 a {
   color: black;
 }
</style>