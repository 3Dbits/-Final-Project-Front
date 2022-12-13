<template>
  <footer class="footer">
    <div class="content has-text-centered">
      <p>
        <strong>BookLike</strong> by <a href="/">Book Crew</a>. The webpage is financed by
        <a href="https://www.telekom.com/en">Deutsche Telekom</a>.
      </p>
      <p>
        <font-awesome-icon icon="fa-brands fa-square-twitter" id="socialIcons"/>
        <font-awesome-icon icon="fa-brands fa-square-facebook" id="socialIcons"/>
        <font-awesome-icon icon="fa-brands fa-square-github" id="socialIcons"/>
        <font-awesome-icon icon="fa-brands fa-linkedin" id="socialIcons"/>
        <font-awesome-icon icon="fa-brands fa-tiktok" id="socialIcons"/>
        <font-awesome-icon icon="fa-brands fa-instagram" id="socialIcons"/>
        <font-awesome-icon icon="fa-brands fa-twitch" id="socialIcons"/>
      </p>
    </div>
  </footer>
</template>

<script>
export default {
  name: "Footer"
}
</script>

<style scoped>
 #socialIcons {
   padding-left: 5px;
 }
</style>