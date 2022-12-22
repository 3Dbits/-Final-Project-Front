<template>
  <div id="minheight">
    <br>
    <div class="field">
      <div v-if="friendAdded" class="notification is-primary" role="alert">
        <button class="delete" @click='goHome'></button>
        Successfully followed user {{ users[0].username }}!
      </div>
    </div>

    <div class="searchForm" v-if="!friendAdded">
      <nav class="panel is-primary">
        <p class="panel-heading">
          Search:
        </p>
        <form novalidate @submit.prevent="getUser">
          <div class="panel-block">
            <p class="control has-icons-left">
              <input id="searchUsername" v-model="searchUsername" class="input is-primary" placeholder="Search username"
                     type="text">
              <span class="icon is-left">
        <font-awesome-icon icon="fa-solid fa-magnifying-glass"/>
      </span>
            </p>
          </div>
          <p class="panel-tabs">
            <a>Username</a>
          </p>
          <a class="panel-block is-active" v-for="user in users" @click="addFriend(user.id)">
          <span class="panel-icon">
       <img src="https://ps.w.org/add-to-any/assets/icon-256x256.png?rev=972738" alt="bookcover">
        </span>
            <div><strong>Name: </strong>{{ user.userInfo.firstName }} {{ user.userInfo.lastName }}</div>
            <div><strong>
              Username: </strong>{{ user.username }}
            </div>
          </a>

          <a v-if="noUser" class="panel-block is-active">
            <strong>No user found! </strong>
          </a>

          <div class="panel-block">
            <button class="button is-primary is-outlined is-fullwidth" type="submit">
              <strong>Search</strong>
            </button>
          </div>
        </form>
      </nav>
    </div>
  </div>
</template>

<!--<div v-for="user in users" :key="user.id">-->
<!--<p>-->
<!--  {{user.userInfo.firstName}}-->
<!--</p>-->
<!--</div>-->

<script>
import authHeader from "@/services/auth-header";

export default {
  name: "FriendsPage",
  data() {
    return {
      users: [],
      searchUsername: "",
      noUser: false,
      friendAdded: false,
    };
  },
  methods: {
    async getUser() {
      // Fetch or Axios
      try {
        // Fetch returns a promise ( asynchronous)
        let response = await fetch("/api/userinfo/" + this.searchUsername, {
          headers: authHeader()
        });
        this.users = await response.json();
        this.noUser = this.users[0] === undefined;
      } catch (error) {
        console.log("Error=", error);
      }
    },
    async addFriend(id) {
      // Fetch or Axios
      try {
        // Fetch returns a promise ( asynchronous)
        let response = await fetch("/api/friends/add/" + id, {
          method: "POST",
          headers: authHeader()
        });
        // this.$router.push("/home");
        this.friendAdded = true;
      } catch (error) {
        console.log("Error=", error);
      }
    },
    goHome() {
      this.$router.push("/home");
    }
  },
}
</script>

<style scoped>
/*.panel-block {*/
/*  display: flex;*/
/*  flex-direction: row;*/
/*  flex-wrap: wrap;*/
/*  width: 100%;*/
/*}*/
.searchForm, .field {
  max-width: 50%;
  margin: auto;
}
#minheight {
  min-height: 750px;
}
</style>