<template>
<br>
  <div class="searchForm">
  <nav class="panel">
    <p class="panel-heading">
      Search:
    </p>
    <form novalidate @submit.prevent="getBooks">
    <div class="panel-block">
      <p class="control has-icons-left">
        <input class="input" type="text" placeholder="Search" id="searchTitle" v-model="searchTitle">
        <span class="icon is-left">
        <font-awesome-icon icon="fa-solid fa-magnifying-glass" />
      </span>
      </p>
    </div>
      <p class="panel-tabs">
        <a :class="searchWay1" @click="searchTerm">Title</a>
        <a :class="searchWay2" @click="searchTerm">Author</a>
        <a :class="searchWay3" @click="searchTerm">ISBN</a>
      </p>

      <router-link :to="{name: 'PostPage', query: {isbn: book.isbn}}" class="panel-block is-active" v-for="book in books" :key="book.id">
    <span class="panel-icon is-size-1">
       <img :src=book.smallThumbnail alt="bookcover" v-if='book.smallThumbnail !== "none"'>
       <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/a/ac/No_image_available.svg/2048px-No_image_available.svg.png" alt="bookcover" v-if='book.smallThumbnail === "none"'>
    </span>
        <div><strong>Title: </strong>{{ book.title }}</div>
        <div v-if="book.authors[0].name !== undefined"><strong> Author: </strong>{{ book.authors[0].name }}</div>
      </router-link>

      <a class="panel-block is-active" v-if="noBook">
    <span class="panel-icon is-size-1">
       <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSzB0JclxHhto76WHFWYNBoqs785MCJHadtkg&usqp=CAU" alt="bookcover">
    </span>
        <strong>No book found! </strong>
      </a>

      <div class="panel-block">
        <button class="button is-link is-outlined is-fullwidth" type="submit">
          Search
        </button>
      </div>
      </form>
  </nav>
  </div>
</template>

<script>
import authHeader from "@/services/auth-header";

export default {
  name: "Search",
  data() {
    return {
      books: [],
      urlAddOn: "?bookName=",
      searchTitle: "Search",
      searchWay1: "is-active",
      searchWay2: "2",
      searchWay3: "3",
      noBook: false,
    };
  },
  methods: {
    async getBooks() {
      // Fetch or Axios
      try {
        // Fetch returns a promise ( asynchronous)
        let response = await fetch("http://localhost:8080/api/book/search" + this.urlAddOn + this.searchTitle.replace(" ", "+"), {
          headers: authHeader()
        });
        this.books = await response.json();
        this.noBook = this.books[0] === undefined;
      } catch (error) {
        console.log("Error=", error);
      }
    },
    searchTerm(e) {
      // console.log(e);
      // console.log(e.target.attributes[0].nodeValue);
      if (e.target.attributes[0].nodeValue === "is-active") {
        console.log("is active, pa nista")
        return;
      }
      if (e.target.attributes[0].nodeValue === "2") {
        this.searchWay1 = "1";
        this.searchWay3 = "3";
        this.urlAddOn = "?bookAuthor=";
        this.searchWay2 = "is-active";
        return;
      }
      if (e.target.attributes[0].nodeValue === "3") {
        this.searchWay1 = "1";
        this.searchWay2 = "2";
        this.urlAddOn = "?bookIsbn=";
        this.searchWay3 = "is-active";
        return;
      }
      if (e.target.attributes[0].nodeValue === "1") {
        this.searchWay2 = "2";
        this.searchWay3 = "3";
        this.urlAddOn = "?bookName=";
        this.searchWay1 = "is-active";
        return;
      }

    }
  }
}
</script>

<style scoped>
.searchForm {
  max-width: 50%;
  margin: auto;
}
</style>