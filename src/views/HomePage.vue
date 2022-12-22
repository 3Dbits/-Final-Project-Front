<template>
<div id="background">
  <div id="maxheightset">
    <h1 id="titleNew">Posts:</h1>
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
<!--        <router-link :to="{name: 'PostPage', query: {id: post.id}}">-->
          <article class="media">
            <div class="media-left">
              <figure class="image is-64x64">
                <img :src=post.book.smallThumbnail alt="bookcover" v-if='post.book.smallThumbnail !== "none"'>
              </figure>
            </div>
            <div class="media-content">
              <router-link :to="{name: 'PostPage', query: {id: post.id}}">
              <div class="content" >
                <p>
                  <strong>{{ post.book.title }}</strong> by <strong
                    v-for="author in post.book.authors">{{ author.name }}</strong>
                  <br>
                  <small>{{ post.userInfo.firstName }} {{ post.userInfo.lastName }}</small> <small>at
                  {{ post.createAt.substr(0, 10) }}</small>
                  <br>
                  {{ post.content }}
                </p>
              </div>
              </router-link>
              <nav class="level is-mobile">
                <div class="level-left">
                  <a class="level-item" aria-label="like">
            <span class="icon is-small" @click="like(post.id)">
              <font-awesome-icon icon="fa-solid fa-hand-holding-heart"/>
            </span>
                  </a>
                  <a class="level-item" aria-label="like">
            <span class="icon is-small">
              {{ post.likes }}
            </span>
                  </a>
                </div>
              </nav>
            </div>
          </article>
<!--        </router-link>-->
      </div>
    </div>
    <div class="box" v-if="posts.length === 0 & loading">
      <article class="media">
        <div class="content">
          <p>
            No posts!
          </p>
          <p>
            Create new post or follow somebody to see some posts!
          </p>
        </div>
      </article>
    </div>
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
      loading: false,
      isLiked: false,
    };
  },
  methods: {
    async getBooks() {
      // Fetch or Axios
      try {
        // Fetch returns a promise ( asynchronous)
        let response = await fetch("/api/post/all", {
          headers: authHeader()
        });
        this.posts = await response.json();
        this.posts.reverse();

      } catch (error) {
        console.log("Error=", error);
      }
      this.loading = true;
    },
    async like(idPost) {
      // Fetch or Axios
      if (this.isLiked) {
        this.dislike(idPost);
      } else {
        try {
          // Fetch returns a promise ( asynchronous)
          let response3 = await fetch("/api/post/like/" + idPost, {
            method: "POST",
            headers: authHeader(),
          });
          this.getBooks();
          this.isLiked = true;
        } catch (error) {
          console.log("Error=", error);
        }
      }
    },
    async dislike(idPost2) {
      // Fetch or Axios
      try {
        // Fetch returns a promise ( asynchronous)
        let response3 = await fetch("/api/post/dislike/" + idPost2, {
          method: "POST",
          headers: authHeader(),
        });
        this.getBooks();
        this.isLiked = false;
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
 #titleNew {
   margin-left: 200px;
   font-weight: bolder;
   font-size: x-large;
 }
 #maxheightset {
   min-height: 700px;
 }
 #background {
   /*background-image: url("../6191149.jpg");*/
   /*background-repeat: no-repeat;*/
   /*background-size: contain;*/
 }
</style>