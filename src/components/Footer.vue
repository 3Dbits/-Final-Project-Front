<template>
  <footer class="footer">
    <div class="content has-text-centered">
      <p>
        <strong>BookLike</strong> by <a href="/">Book Crew</a>. The webpage is financed by
        <a href="https://www.telekom.com/en">Deutsche Telekom</a>.
      </p>
      <p>
        <a href="/#">
          <span>
          <font-awesome-icon icon="fa-brands fa-square-twitter" size="2x" id="socialIcons"/>
        </span>
        </a>
        <a href="/#">
        <span >
          <font-awesome-icon icon="fa-brands fa-square-facebook" size="2x" id="socialIcons"/>
        </span>
        </a>
        <a href="/#">
        <span >
          <font-awesome-icon icon="fa-brands fa-square-github" size="2x" id="socialIcons"/>
        </span>
        </a>
        <a href="/#">
        <span >
          <font-awesome-icon icon="fa-brands fa-linkedin" size="2x" id="socialIcons"/>
        </span>
        </a>
        <a href="/#">
        <span >
          <font-awesome-icon icon="fa-brands fa-tiktok" size="2x" id="socialIcons"/>
        </span>
        </a>
        <a href="/#">
        <span >
          <font-awesome-icon icon="fa-brands fa-instagram" size="2x" id="socialIcons"/>
        </span>
        </a>
        <a href="/#">
        <span >
          <font-awesome-icon icon="fa-brands fa-twitch" size="2x" id="socialIcons" />
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
   color: rgb(0, 196, 167);
 }
</style>