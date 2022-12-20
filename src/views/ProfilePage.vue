<script>
import authHeader from "@/services/auth-header";
import FriendList from "../components/FriendList.vue";
import PostList from "../components/PostList.vue";
import UserInfo from "../components/UserInfo.vue";

export default {
  name: "ProfilePage",
components: {
    UserInfo,
    PostList,
    FriendList
    }
}
</script>
<template>
  <strong> My profile </strong>
  <div class="tile is-ancestor">
    <div class="tile is-vertical is-8">
      <div class="tile">
        <div class="tile is-parent is-vertical">
          <article class="tile is-child notification is-primary">
            <article class="tile is-child notification is-warning">
              <userInfo></userInfo>

              <img src="../components/lista_uredaja.jpg">
            </article>
          </article>
        </div>
      </div>
    </div>
    <article class="tile is-child notification is-danger">
      <p class="title">User posts</p>
      <h5> List of user posts</h5>

      <postList></postList>
    </article>
  </div>
  <div class="tile is-parent">
    <article class="tile is-child notification is-success">
      <div class="content">
        <p class="title">My friends</p>
        <p class="subtitle">Friend List</p>

        <FriendList></FriendList>

      </div>
    </article>
  </div>
</template>
