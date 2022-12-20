<script>
import authHeader from "../services/auth-header";

export default {
  data() {
    return {
      friends: {},
    }
  },
  methods: {
    async getFriends() {
      // Fetch or Axios
      try {
        // Fetch returns a promise ( asynchronous)
        let response = await fetch("http://localhost:8080/api/friends/", {
          headers: authHeader()
        });
        this.friends = await response.json();
      } catch (error) {
        console.log("Error=", error);
      }
    },
  },
  created() {
    this.getFriends()
  }
}
</script>

<template>
  <div class="user-info__item">
    <h4 class="user-info__detail">
						<span class="user-info__icon">
							<i class="fa fa-user-friends" />
						</span>
    </h4>

  </div>
  <div class="user-list__wrapper page-inner">
    <transition-group
        tag="ul"
        name="slide"
        class="user-list">
    <ul>
      <li v-for="friend in friends" :key="friend.id">
        {{ friend.firstName }} {{friend.lastName}}
      </li>
    </ul>
    </transition-group>
  </div>
</template>