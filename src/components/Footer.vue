<template>
  <footer class="footer">
    <div class="content has-text-centered">
      <p>
        <strong>BookLike</strong> by <a href="/">Book Crew</a>. The webpage is financed by
        <a href="https://www.telekom.com/en">Deutsche Telekom</a>.
      </p>
      <p>
        <a href="/#">
          <span @mouseover="isHovering11 = true" @mouseout="isHovering11 = false">
          <font-awesome-icon icon="fa-brands fa-square-twitter" size="2x" id="socialIcons" v-if="!isHovering11"/>
          <font-awesome-icon icon="fa-brands fa-square-twitter" size="2x" id="socialIcons" flip v-if="isHovering11"/>
        </span>
        </a>
        <a href="/#">
        <span @mouseover="isHovering12 = true" @mouseout="isHovering12 = false">
          <font-awesome-icon icon="fa-brands fa-square-facebook" size="2x" id="socialIcons" v-if="!isHovering12"/>
          <font-awesome-icon icon="fa-brands fa-square-facebook" size="2x" id="socialIcons" flip v-if="isHovering12"/>
        </span>
        </a>
        <a href="/#">
        <span @mouseover="isHovering13 = true" @mouseout="isHovering13 = false">
          <font-awesome-icon icon="fa-brands fa-square-github" size="2x" id="socialIcons" v-if="!isHovering13"/>
          <font-awesome-icon icon="fa-brands fa-square-github" size="2x" id="socialIcons" flip v-if="isHovering13"/>
        </span>
        </a>
        <a href="/#">
        <span @mouseover="isHovering14 = true" @mouseout="isHovering14 = false">
          <font-awesome-icon icon="fa-brands fa-linkedin" size="2x" id="socialIcons" v-if="!isHovering14"/>
          <font-awesome-icon icon="fa-brands fa-linkedin" size="2x" id="socialIcons" flip v-if="isHovering14"/>
        </span>
        </a>
        <a href="/#">
        <span @mouseover="isHovering15 = true" @mouseout="isHovering15 = false">
          <font-awesome-icon icon="fa-brands fa-tiktok" size="2x" id="socialIcons" v-if="!isHovering15"/>
          <font-awesome-icon icon="fa-brands fa-tiktok" size="2x" id="socialIcons" flip v-if="isHovering15"/>
        </span>
        </a>
        <a href="/#">
        <span @mouseover="isHovering16 = true" @mouseout="isHovering16 = false">
          <font-awesome-icon icon="fa-brands fa-instagram" size="2x" id="socialIcons" v-if="!isHovering16"/>
          <font-awesome-icon icon="fa-brands fa-instagram" size="2x" id="socialIcons" flip v-if="isHovering16"/>
        </span>
        </a>
        <a href="/#">
        <span @mouseover="isHovering17 = true" @mouseout="isHovering17 = false">
          <font-awesome-icon icon="fa-brands fa-twitch" size="2x" id="socialIcons" v-if="!isHovering17"/>
          <font-awesome-icon icon="fa-brands fa-twitch" size="2x" id="socialIcons" flip v-if="isHovering17"/>
        </span>
        </a>
      </p>
    </div>
  </footer>
</template>

<script>

export default {
  name: "Footer",
  data() {
    return {
      className: "a",
      isHovering11: false,
      isHovering12: false,
      isHovering13: false,
      isHovering14: false,
      isHovering15: false,
      isHovering16: false,
      isHovering17: false,
    }
  },
  methods: {
    changeClass(){
      this.className = "fa-flip";
      setTimeout( function () {
        console.log("test");
        this.className = "a";
      }, 3000);
    },
    changeName() {
      this.className = "a";
    }
  }
}

</script>

<style scoped>
 #socialIcons {
   padding-left: 5px;
 }
 a:link {
   color: black;
 }
</style>