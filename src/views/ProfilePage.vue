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
<!--  <strong> My profile </strong>-->
  <div id="widthset">
    <div class="tile is-ancestor" >
      <div class="tile is-vertical is-8">
        <div class="tile">
          <div class="tile is-parent is-vertical">
            <article class="tile is-child notification has-background-danger-light">
              <article class="tile is-child notification  has-background-primary-light">
                <userInfo></userInfo>

            </article>
          </article>
        </div>
      </div>
    </div>
    <article class="tile is-child notification has-background-link-light">
      <h5>Following</h5>
      <FriendList></FriendList>

    </article>
  </div>
  <div class="tile is-parent">
    <article class="tile is-child notification has-background-success-light">
      <div class="content">


        <postList></postList>

        </div>
      </article>
    </div>
  </div>
</template>
<style>
#widthset {
  max-width: 80%;
  margin: auto;
}


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
  background: #0fb59d;
  color: #fff;
  border-color: #89c4bb;
}

.btn-primary:active, .btn-primary:hover, .btn-primary.focus, .btn-primary.active {
  background: #00c4a7 !important;
  border-color: #00e6c4 !important;
}

.btn-outline-primary {
  background: transparent;
  color: #0fb59d;
  border-color: #89c4bb;
}

.btn-outline-primary:active, .btn-outline-primary:hover, .btn-outline-primary.focus, .btn-outline-primary.active {
  background: #00c4a7 !important;
  border-color: #00e6c4 !important;
  color: #fff;
}

</style>