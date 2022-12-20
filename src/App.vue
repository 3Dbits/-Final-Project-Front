<template>
  <Header/>

  <router-view/>

  <Footer/>

</template>

<script>
import Header from "@/components/Header.vue";
import Footer from "@/components/Footer.vue";
import FriendList from "@/components/FriendList.vue";
import PostList from "@/components/PostList.vue";
import UserInfo from "@/components/UserInfo.vue";
import ProfilePage from "./views/ProfilePage.vue"


export default {
  data() {
    return {

    }
  },
  components: {
    Footer,
    Header,
    ProfilePage,
    PostList,
    UserInfo,
    FriendList
  },
};
</script>

<style>
</style>
