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
        <a class="is-active">Title</a>
        <a>Author</a>
        <a>ISBN</a>
      </p>

      <router-link :to='"/post?isbn=" + book.isbn' class="panel-block is-active" v-for="book in books" :key="book.id">
    <span class="panel-icon is-size-2">
       <img :src=book.smallThumbnail alt="bookcover" v-if='book.smallThumbnail !== "none"'>
    </span>
        <strong>Title: </strong>{{ book.title }}
        <strong>Author: </strong>{{ book.authors[0].name }}
      </router-link>

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
      } catch (error) {
        console.log("Error=", error);
      }
    },
    getString(value) {

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