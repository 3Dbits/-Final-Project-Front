<template>
  <nav class="navbar" role="navigation" aria-label="main navigation">
    <div class="navbar-brand">
      <a class="navbar-item" >
        <router-link to="/">
        <img src="/imgbin_book-png.png" width="112" height="28">
        </router-link>
      </a>

      <a role="button" class="navbar-burger" aria-label="menu" aria-expanded="false" data-target="navbarBasicExample">
        <span aria-hidden="true"></span>
        <span aria-hidden="true"></span>
        <span aria-hidden="true"></span>
      </a>

    </div>

    <div id="navbarBasicExample" class="navbar-menu">
      <div class="navbar-start">
          <router-link to="/home" v-if="currentUser" class="navbar-item">Home</router-link>

        <div class="navbar-item has-dropdown is-hoverable" v-if="currentUser">
          <a class="navbar-link">
            More
          </a>

          <div class="navbar-dropdown">
              <router-link class="navbar-item" to="/user">User</router-link>
              <router-link to="/admin" class="navbar-item" v-if="showAdminBoard">Admin Board</router-link>
          </div>
        </div>
      </div>

      <div class="navbar-end">
        <div class="navbar-item">
          <div class="buttons" v-if="!currentUser">
            <router-link to="/register" class="button is-primary">
              <strong>Sign Up</strong>
            </router-link>
            <router-link to="/login" class="button is-light">Login</router-link>
          </div>
          <div class="buttons" v-if="currentUser">
            <router-link to="/profile" class="button is-primary">{{ currentUser.username }}</router-link>
            <a @click.prevent="logOut" class="button is-light">LogOut</a>
          </div>
        </div>
      </div>
    </div>
  </nav>
</template>

<script>
export default {
  name: "Header",
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
}

document.addEventListener('DOMContentLoaded', () => {

  // Get all "navbar-burger" elements
  const $navbarBurgers = Array.prototype.slice.call(document.querySelectorAll('.navbar-burger'), 0);

  // Add a click event on each of them
  $navbarBurgers.forEach( el => {
    el.addEventListener('click', () => {

      // Get the target from the "data-target" attribute
      const target = el.dataset.target;
      const $target = document.getElementById(target);

      // Toggle the "is-active" class on both the "navbar-burger" and the "navbar-menu"
      el.classList.toggle('is-active');
      $target.classList.toggle('is-active');

    });
  });

});
</script>

<style scoped>

</style>