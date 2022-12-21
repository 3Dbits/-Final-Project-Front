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


            </article>
          </article>
        </div>
      </div>
    </div>
    <article class="tile is-child notification is-danger">

      <postList></postList>

    </article>
  </div>
  <div class="tile is-parent">
    <article class="tile is-child notification is-success">
      <div class="content">
        <h5>Following</h5>


        <FriendList></FriendList>

      </div>
    </article>
  </div>
</template>
