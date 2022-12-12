<template>
  <section>
    <nav>
<!--      MC there is <li> thrown in here, as it is just example its not problem now-->
      <a href="/">BookApp</a>
      <li>
        <router-link to="/home">Home</router-link>
      </li>
      <li v-if="showAdminBoard">
        <router-link to="/admin">Admin Board</router-link>
      </li>
      <li>
        <router-link v-if="currentUser" to="/user">User</router-link>
      </li>

      <div v-if="!currentUser">
        <li>
          <router-link to="/register">Sign Up</router-link>
        </li>
        <li>
          <router-link to="/login">Login</router-link>
        </li>
      </div>

      <div v-if="currentUser">
        <li>
          <router-link to="/profile">{{ currentUser.username }}</router-link>
        </li>
        <li>
          <a @click.prevent="logOut">LogOut</a>
        </li>
      </div>
    </nav>
    <router-view/>
  </section>
</template>

<script>
export default {
  computed: {
    currentUser() {
      return this.$store.state.auth.user;
    },
    showAdminBoard() {
      if (this.currentUser && this.currentUser['roles']) {
        return this.currentUser['roles'].includes('ROLE_ADMIN');
      }

      return false;
    }
  },
  methods: {
    logOut() {
      this.$store.dispatch('auth/logout');
      this.$router.push('/login');
    }
  }
};
</script>
