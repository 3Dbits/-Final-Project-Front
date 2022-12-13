<template>
  <section id="container">
    <img src="/jaredd-craig-HH4WBGNyltc-unsplash.jpg" id="image" alt="index book picture">
    <div class="card centered">
      <div class="card-content">
        <p class="title">
          “That’s the thing about books. They let you travel without moving your feet.”
        </p>
        <p class="subtitle">
          Jhumpa Lahiri
        </p>
      </div>
    </div>
    <div></div>
    <div></div>
    <div></div>
  </section>
</template>

<script>
export default {
  name: "indexPage"
}
</script>

<style scoped>
  img {
    width: 100%;
  }
  #container {
    position: relative;
    text-align: center;
    color: white;
  }
  .centered {
    position: absolute;
    top: 25%;
    left: 50%;
    transform: translate(-50%, -50%);
  }
</style>