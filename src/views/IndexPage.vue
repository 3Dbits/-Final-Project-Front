<template>
  <section class="container2">
    <img id="image" alt="index book picture" src="/jaredd-craig-HH4WBGNyltc-unsplash.jpg">
    <div class="card has-background centered">
      <div class="card-content">
        <p class="has-text-white title">
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
          <img src="/Screenshot_360.png" id="firstpic">
        </div>
        <div>
          <br><br><br><br><br><br><br><br>
          <h1 class="indexText">
            Search for your favorite books with our new search function.
          </h1>
        </div>
        <div>
          <br><br><br><br>
          <h1 class="indexText" id="rightspace">
            Tell your friends what you think about book and find inspiration for your new book.
          </h1>
        </div>
        <div class="item2">
          <img src="/homepagepic/kindpng_4808540.png">
        </div>
      </div>
    </div>
  </section>

  <section class="showPicture">
    <div id="image-track">
      <img class="image" src="/img-gaetano-1_142151851246.jpg" alt="picture" draggable="false"/>
      <img class="image" src="/3b47d124002685f2a3c67e47383232c7.jpg" alt="picture" draggable="false"/>
      <img class="image" src="/invisibleman-1509049531-640x996.jpg" alt="picture" draggable="false"/>
      <img class="image" src="/bravenewworld.jpg" alt="picture" draggable="false"/>
      <img class="image" src="/gatsby-original2.jpg" alt="picture" draggable="false"/>
      <img class="image" src="/ClockworkCovers_0006.jpg" alt="picture" draggable="false"/>
    </div>
  </section>
</template>

<script>
export default {
  name: "indexPage",
}
</script>

<style scoped>
img {
  /*width: 100%;*/
}
.title, .subtitle{
  text-shadow: 2px 2px 2px black;
}
.container2 {
  position: relative;
  text-align: center;
}
.container3 {
  /*background-color: #fff;*/
  /*background-image: linear-gradient(90deg, transparent 79px, #abced4 79px, #abced4 81px, transparent 81px),*/
  /*linear-gradient(#eee .1em, transparent .1em);*/
  /*background-size: 100% 1.2em;*/
  background-color: #ffffff;
  background-image:  repeating-radial-gradient( circle at 0 0, transparent 0, #ffffff 9px ), repeating-linear-gradient( #c2c2c255, #c2c2c2 );
}
.widthSet {
  /*max-width: 80%;*/
}
.gridSet {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  grid-row-gap: 20px;
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
.showPicture {
  height: 80vh;
  width: 100vw;
  background-color: black;
  margin: 0rem;
  overflow: hidden;
}
#image-track > .image {
  width: 40vmin;
  height: 56vmin;
  object-fit: cover;
  object-position: center;
}
#image-track {
  display: flex;
  gap: 4vmin;
  /*position: absolute;*/
  left: 50%;
  top: 50%;
  transform: translate(0.5%, 20%);
}
.indexText {
  display: grid;
  font-weight: bolder;
  font-family: "Helvetica Neue",fantasy;
  font-size: xx-large;
  /*align-content: center;*/
  max-width: 60%;
}
#firstpic {
  max-width: 80%;
  box-shadow: 1px 1px 2px gray;
  border-radius: 20px;
}
#rightspace {
  /*text-align: right;*/
  margin-left: 270px;
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