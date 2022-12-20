<script>
import authHeader from "../services/auth-header";
import moment from 'moment';
export default {
  data() {
    return {
      user: {},
      userInfos : {},
    }
  },
  methods: {
    getFormattedDate(date) {
      return moment(date).format("DD. MMM YYYY")
    },
    goToProfilePage() {
      // Navigate to the profile page
      this.$router.push('/userInfo')
    },
    async getUserInfos() {
      // Fetch or Axios
      try {
        // Fetch returns a promise ( asynchronous)
        let response = await fetch("http://localhost:8080/api/userinfo/", {
          headers: authHeader()
        });
        this.userInfos = await response.json();
      } catch (error) {
        console.log("Error=", error);
      }
    },
  },
  created() {
    this.getUserInfos()
  }
}
</script>

<template>
  <div class="user-info">
      </div>

  <div class="user-info__group">
    <div class="userinfo__item">
      <h4 class="user-info__label" >
      <span class="user-info__icon">
        <i class="fa fa-user"/>
      </span>
      <strong>Name:</strong>
      </h4>

      <p class="user-info__data" >
        {{userInfos.firstName}} {{userInfos.lastName}}
      </p>
    </div>
    <div class="user-info__item">
      <h4 class="user-info__detail">
						<span class="user-info__icon">
							<i class="fa-clock" />
						</span>
        <strong>Sign-Up date:</strong>
      </h4>
      <p class="user-info__data">
        {{getFormattedDate(userInfos.signupDate)}}
      </p>
    </div>
    <div class="user-info__item">
      <h4 class="user-info__detail">
						<span class="user-info__icon">
							<i class="fa fa-clock" />
						</span>
        <strong>Date of birth:</strong>
      </h4>
      <p class="user-info__data">
        {{getFormattedDate(userInfos.dateOfBirth) }}
      </p>
    </div>
    <div class="user-info__item">
      <h4 class="user-info__detail">
						<span class="user-info__icon">
							<i class="fa fa-book" />
						</span>
        <strong>Favorite book:</strong>
      </h4>
      <p class="user-info__data">
        {{userInfos.bookId}}
      </p>
    </div>


  </div>
</template>