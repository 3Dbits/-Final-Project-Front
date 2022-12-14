<template>
  <section class="container2">
    <img id="image" alt="index book picture" src="/jaredd-craig-HH4WBGNyltc-unsplash.jpg">
    <div class="card has-background centered">
      <div class="card-content">
        <p class="title has-text-white">
          “That’s the thing about books. They let you travel without moving your feet.”
        </p>
        <p class="subtitle has-text-white">
          - Jhumpa Lahiri
        </p>
      </div>
    </div>
  </section>
  <section class="container3">
    <div class="widthSet">
      <div class="gridSet">
        <div class="item1">
          <!--        add style to see 2 rows, need to be removed-->
          <img src="/homepagepic/imgbin_table-bookcase-floating-shelf-furniture-png.png" style="height: 500px">
        </div>
        <div>
          <p>
            Test
          </p>
        </div>
        <div>
          <p>
            Test
          </p>
        </div>
        <div class="item2">
          <img src="/homepagepic/kindpng_4808540.png">
        </div>
      </div>
    </div>
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
.container2 {
  position: relative;
  text-align: center;
}
.container3 {
  background-color: #fff;
  background-image: linear-gradient(90deg, transparent 79px, #abced4 79px, #abced4 81px, transparent 81px),
  linear-gradient(#eee .1em, transparent .1em);
  background-size: 100% 1.2em;
}
.widthSet {
  /*max-width: 80%;*/
}
.gridSet {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
}
.container3 div {
  text-align: center;
}
.centered {
  position: absolute;
  top: 23%;
  left: 50%;
  transform: translate(-50%, -50%);
}
.card {
  background-color: transparent;
  box-shadow: none;
}
.item1 {
  grid-column-start: 1;
  grid-column-end: 3;
}
.item2 {
  grid-row-start: 2;
  grid-column-start: 2;
  grid-column-end: 4;
}

@media screen and (max-width: 800px) {
  .title {
    font-size: 1rem;
    font-weight: 500;
    line-height: 1;
  }

  .subtitle {
    font-size: 0.75rem;
    font-weight: 300;
    line-height: 1;
  }
}
</style>