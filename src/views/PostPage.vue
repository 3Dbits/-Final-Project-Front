<template>
<!--  <nav class="navbar is-white">-->

<!--    <div class="container">-->

<!--      <div class="navbar-menu">-->
<!--        <div class="navbar-start">-->
<!--          <a class="btn btn-outline-primary">Popular</a>-->
<!--          <a class="btn btn-outline-primary">Latest</a>-->
<!--          <a class="btn btn-outline-primary">Rising</a>-->
<!--        <div class="navbar-end">-->
<!--        <div class="navbar-item">-->
<!--        </div>-->
<!--        </div>-->
<!--        </div>-->
<!--      </div>-->
<!--    </div>-->
<!--  </nav>-->

  <!--slika unutar aside classa-->
  <section class="container">
    <div class="columns">
      <div class="column is-3">
        <aside class="menu">
          <p class="menu-label">
            <br>
            Book Information
          </p>
          <ul class="menu-list">

            <li>
            <span class="media-right">


              <img v-if="isbnParams!==undefined && books[0].smallThumbnail!=='none'" :src=books[0].smallThumbnail
                   alt="bookcover">
              <img v-if="isbnParams===undefined && post.book?.smallThumbnail==='none'"
                   alt="dummypicture"
                   src="https://www.mswordcoverpages.com/wp-content/uploads/2018/10/Book-cover-page-1-CRC.png">
              <!--dodala usklicnike prije tocke kako bi nastavio provjeru bez da prvo zna da postoji  -->
              <img v-if="isbnParams!==undefined && books[0]?.smallThumbnail==='none'"
                   src="https://www.mswordcoverpages.com/wp-content/uploads/2018/10/Book-cover-page-1-CRC.png">
              <img v-if="isbnParams===undefined && post.book?.smallThumbnail!=='none'" :src=post.book?.smallThumbnail
                   alt="bookcover">
            </span>
            </li>

            <section v-for="book in books" v-if="isbnParams!==undefined" :key="book.id">
              <li><span class="btn btn-outline-primary ">Title: {{ book.title }}</span></li>
              <li><span class="btn btn-outline-primary ">Publisher: {{ book.publisher }}</span></li>
              <li><span class="btn btn-outline-primary ">Page number: {{ book.pageNumber }}</span></li>
              <li><span class="btn btn-outline-primary ">Language : {{ book.language }}</span></li>
              <a v-if="book.pdf!=undefined" :href=book.pdf target="_blank">
                <figure class="image is-64x64">
                  <img alt="Image"
                       src=" https://cdn1.iconfinder.com/data/icons/education-flat-icons-shadow/96/50-512.png"/>
                </figure>
              </a>
            </section>


            <section v-if="isbnParams===undefined">
              <li><span class="btn btn-outline-primary ">Title: {{ post.book?.title }}</span></li>
              <li><span class="btn btn-outline-primary ">Publisher : {{ post.book?.publisher }}</span></li>
              <li><span class="btn btn-outline-primary ">Page number : {{ post.book?.pageNumber }}</span></li>
              <li><span class="btn btn-outline-primary ">Language : {{ post.book?.language }}</span></li>
              <a v-if="post.book?.pdf!=undefined" :href=post.book?.pdf target="_blank">
                <figure class="image is-64x64">
                  <img alt="Image"
                       src="https://cdn1.iconfinder.com/data/icons/education-flat-icons-shadow/96/50-512.png"/>
                </figure>
              </a>
            </section>
          </ul>
        </aside>
      </div>


      <div class="column is-10">
        <div class="box content">
          <article class="post">
            <span style="text-align: center">
               <br>
            <h1>{{ books[0]?.title }}</h1>
             <h1>{{ post.book?.title }}</h1>
             <h1>  {{ $route.params.id }}</h1>
            <h3>{{ post.content }}</h3>


              <!--              /////POST//////-->

               <br>
              </span>
            <div class="media">

              <div class="content">
                <!--                ///ako nema posta otvori box za upis novog post////////////-->
                <div v-if="postParams === undefined">
                  <div class="column md-6">
                    <form @submit.prevent="setPost">
                      <div class="field">
                        <label class="label is-medium" for="post">Write Post about : <strong>{{
                            books[0]?.title
                          }}</strong></label>
                        <textarea id="content" v-model="newPost.content" class="textarea input is-warning "></textarea>
                      </div>
                      <input class="btn btn-primary w-100 rounded mt-2 is-alt" type="submit" value="Create New Post">
                    </form>
                  </div>
                </div>
              </div>
            </div>
<!--            <div class="media">-->

<!--              <div class="content">-->
<!--                <div v-if="post !== undefined">-->
<!--                  <div class="column md-6">-->
<!--                    {{ post.content }}-->
<!--                  </div>-->
<!--                </div>-->
<!--              </div>-->
<!--            </div>-->
          </article>

          <!--          Comments-->
          <div v-if="postParams !==undefined" class="box content" style="margin: auto">
            <article class="post">
            <span style="text-align: center">
            <h1>{{ books[0]?.title }}</h1>
              </span>
              <div class="media">

                <div class="content">
                  <div class="column md-6">
                    <form @submit.prevent="getComment">
                      <div class="field">
                        <label class="label is-medium" for="post">Comment Post about : {{ post.book?.title }} </label>
                        <textarea id="content" v-model="comment.content" class="textarea2 input is-warning "></textarea>
                      </div>
                      <input class="btn btn-primary w-100 rounded mt-2 is-alt" href="#" type="submit" value="Send now"/>
                    </form>
                  </div>
                </div>
              </div>
            </article>

            <div v-for="commentFromPost in post.comments.reverse()" :key="post.comments" class="box">
              <article class="media">
                <div class="media-left">
                  <figure class="image is-64x64">
                    <img alt="Image"
                         src="https://images-wixmp-ed30a86b8c4ca887773594c2.wixmp.com/f/61f1b112-2cb0-40b0-a6b9-9ab92066e5c7/d33mwsf-0dd81126-6d91-4b0d-905c-886a1a41566c.png?token=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJ1cm46YXBwOjdlMGQxODg5ODIyNjQzNzNhNWYwZDQxNWVhMGQyNmUwIiwiaXNzIjoidXJuOmFwcDo3ZTBkMTg4OTgyMjY0MzczYTVmMGQ0MTVlYTBkMjZlMCIsIm9iaiI6W1t7InBhdGgiOiJcL2ZcLzYxZjFiMTEyLTJjYjAtNDBiMC1hNmI5LTlhYjkyMDY2ZTVjN1wvZDMzbXdzZi0wZGQ4MTEyNi02ZDkxLTRiMGQtOTA1Yy04ODZhMWE0MTU2NmMucG5nIn1dXSwiYXVkIjpbInVybjpzZXJ2aWNlOmZpbGUuZG93bmxvYWQiXX0.L1TKNejYQvgjxpf-RG78w_VWYwPL4obeec-BqOB-gmw">
                  </figure>
                </div>
                <div class="media-content">
                  <div class="content">
                    <p>
                      <strong>{{ commentFromPost.user.firstName }} {{ commentFromPost.user.lastName }}</strong>
                      <small>{{ commentFromPost.user.username }}</small>
                      <small>{{ post.comment }}</small>
                      <br>
                      <span>{{ commentFromPost.content }}</span>

                    </p>
                  </div>
                </div>
                <nav class="level is-mobile">
                  <div class="level-left">
                    <a aria-label="reply" class="level-item">
                      <span class="icon is-small">
                      <i aria-hidden="true" class="fas fa-reply"></i>
                      </span>
                    </a>
                    <a aria-label="retweet" class="level-item">
            <span class="icon is-small">
              <i aria-hidden="true" class="fas fa-retweet"></i>
            </span>
                    </a>
                    <a aria-label="like" class="level-item">
            <span class="icon is-small">
              <i aria-hidden="true" class="fas fa-heart"></i>
            </span>
                    </a>
                  </div>
                </nav>
              </article>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>

<!--

  //////////////////////////////////////////
  <div class="menu">
    <div class="column is-full">
      <a class="yellow" href="#">Home</a>
      <a class="green" href="#">Blog</a>
      <a class="pink" href="#">Kureshki</a>
      <a class="purple" href="#">Themes</a>
      <a class="blue" href="#">Madenca</a>
      <a class="orange" href="#">Contact</a>
      <a class="darkPurple" href="#">Contact</a>
      <a class="limeShadow" href="#">Contact</a>
      <a class="greenYellow" href="#">Contact</a>
      <a class="tealShadow" href="#">Contact</a>
      <a class="redShadow" href="#">Contact</a>
      <a class="darkPurpleBrown" href="#">Contact</a>
      <a class="cyan" href="#">Contact</a>
      <a class="beige" href="#">Contact</a>
      <a class="green" href="#">Blog</a>
      <a class="blueShadow" href="#">Contact</a>
    </div>
  </div>
-->

</template>
<script>
import authHeader from "@/services/auth-header";

export default {
  name: "PostPage",
  data() {
    return {
      books: [],
      post: Object,
      urlAddOn: "?bookName=",
      name: "Search",
      postParams: undefined,
      isbnParams: undefined,
      CommentList: [],
      comment: {
        content: ""
      },
      comment2: Object,
      PostList: [],
      post1: {
        content: ""
      },
      post2: Object,
      newPost: {
        content: "",
      },

    };
  },
  methods: {
    async getBooks() {
      // Fetch or Axios
      try {
        // Fetch returns a promise ( asynchronous)
        let response = await fetch("/api/book/search?bookIsbn=" + this.isbnParams, {
          headers: authHeader()
        });
        this.books = await response.json();
      } catch (error) {
        console.log("Error=", error);
      }
    },
    async getPosts() {
      // Fetch or Axios
      try {
        // Fetch returns a promise ( asynchronous)
        let response1 = await fetch("/api/post/" + this.postParams, {
          headers: authHeader(),
        });
        this.post = await response1.json();
      } catch (error) {
        console.log("Error=", error);
      }
    },
    async getComment() {
      // Fetch or Axios
      try {
        // Fetch returns a promise ( asynchronous)
        let response2 = await fetch("/api/comment/" + this.postParams, {
          method: "POST",
          headers: authHeader(),
          body: JSON.stringify({
            content: this.comment.content
          }),
        });
        this.comment2 = await response2.json();
        this.getPosts();
      } catch (error) {
        console.log("Error=", error);
      }
    },
    async setPost() {
      // Fetch or Axios
      try {
        // Fetch returns a promise ( asynchronous)
        let response3 = await fetch("/api/post/addNew?bookIsbn=" + this.isbnParams, {
          method: "POST",
          headers: authHeader(),
          body: JSON.stringify({
            content: this.newPost.content,
          }),
        });
        this.goHome();
      } catch (error) {
        console.log("Error=", error);
      }
    },
    goHome() {
      this.$router.push("/home");
    }
  },
  created() {
    // this.getBooks();
    // this.getPosts();
    console.log(this.$route.query.isbn);
    this.postParams = this.$route.query.id;
    this.isbnParams = this.$route.query.isbn;
    if (this.postParams !== undefined) {
      this.getPosts()
    } else {
      this.getBooks()
    }
  },
}


</script>
<style scoped>

/*@import url(http://fonts.googleapis.com/css?family=Open+Sans:400,300,600);*/

* {
  margin: 0;
  padding: 0;
}

body {
  background: #111;
  color: #fff;
  font-family: 'Open sans', sans-serif;
  font-weight: 300;
  font-size: 20pt;
}

a {
  color: #fff;
  text-decoration: none;
}

.menu {
  width: 1200px;
  margin: 30px auto;
}

.menu a {
  width: 260px;
  line-height: 260px;
  display: block;
  margin: 5px;
  text-align: center;
  float: left;
  opacity: 0.3;
}

@media (min-width: 500px) {
  .media {
    display: grid;
    grid-template-columns: fit-content(200px) 1fr;
    grid-template-rows:1fr auto;
    grid-template-areas:
            "image content"
            "image footer";
    grid-gap: 20px;
    margin-bottom: 4em;
  }

  .media-flip {
    grid-template-columns: 1fr fit-content(250px);
    grid-template-areas:
            "content image"
            "footer image";
  }

  .img {
    grid-area: image;
  }

  .content {
    grid-area: content;
  }

  .footer {
    grid-area: footer;
  }
}

/* Button style */
.btn {
  font-size: 14px;
  font-family: "Open Sans", sans-serif;
  text-transform: capitalize;
  padding: 10px 25px;
  border-radius: 50px;
  border: 1px solid;
  position: relative;
  z-index: 1;
  transition: 0.2s ease;
  display: inline-block;
}

.btn:hover, .btn:active, .btn:focus {
  outline: 0;
  box-shadow: none !important;
}

.btn-primary {
  background: #ce8460;
  color: #fff;
  border-color: #ce8460;
}

.btn-primary:active, .btn-primary:hover, .btn-primary.focus, .btn-primary.active {
  background: #ce8460 !important;
  border-color: #ce8460 !important;
}

.btn-outline-primary {
  background: transparent;
  color: #696c6d;
  border-color: #ce8460;
}

.btn-outline-primary:active, .btn-outline-primary:hover, .btn-outline-primary.focus, .btn-outline-primary.active {
  background: #ce8460 !important;
  border-color: #ce8460 !important;
  color: #fff;
}

.btn-outline-light {
  background: transparent;
  color: #696c6d;
  border-color: #ddd;
}

.btn-outline-light:active, .btn-outline-light:hover, .btn-outline-light.focus, .btn-outline-light.active {
  background: #f0f0f0 !important;
  border-color: #ddd !important;
}

body {
  background-color: #fff;
  overflow-x: hidden;
}

.textarea {
  width: 250px;
  height: 200px;
}

.textarea2 {
  margin: auto; /*//za centriranje*/
  height: 100px;
  text-align: left;
  max-width: 70%;
}

::-moz-selection {
  background: #daa287;
  color: #fff;
}

.yellow {
  background: #fdd22a;
}

.blue {
  background: #009fe3;
}

.purple {
  background: #574696;
}

.orange {
  background: #ee7202;
}

.pink {
  background: #e61c67;
}

.green {
  background: #96c11f;
}

.tealShadow {
  background: rgba(0, 174, 239, 0.5);
}

.darkPurple {
  background: rgba(236, 0, 140, 0.3);
}

.limeShadow {
  background: rgba(141, 198, 63, 0.5);
}

.greenYellow {
  background: rgba(255, 242, 0, 0.5);
}

.redShadow {
  background: rgba(237, 28, 36, 0.5);
}

.darkPurpleBrown {
  background: rgba(102, 45, 145, 0.3);
}

.cyan {
  background: rgba(237, 28, 290, 0.5);
}

.beige {
  background: rgba(252, 176, 64, 0.5);
}

.blueShadow {
  background: rgba(0, 174, 239, 0.5);
}

</style>
