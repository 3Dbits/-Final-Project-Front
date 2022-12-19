<template>
<p>Testtt</p>
</template>

<script>
export default {
  name: "PostPage",
  data() {
    return {
     postParams: undefined,
     isbnParams: undefined,
    }
  },
  created() {
    console.log(this.$route.query.isbn);
    this.postParams = this.$route.query.id;
    this.isbnParams = this.$route.query.isbn;
    console.log(this.isbnParams + "test");
  }
}
</script>

<style scoped>

</style>