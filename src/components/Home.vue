<template>
  <div class="col-6">
    <div class="card" style="width: 18rem;">
      <img src="#" class="card-img-top" alt="..." />
      <div class="card-body">
        <h5 class="card-title">Card title</h5>
        <p class="card-text">
          Some quick example text to build on the card title and make up the
          bulk of the card's content.
        </p>
        <a href="#" class="btn btn-primary">Go somewhere</a>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "Home",
  data(){
      return{
        articles: []
      }
  },
  mounted() {
    const URL = `https://newsapi.org/v2/top-headlines?country=ng&apiKey=ee85542cb07b4ad3997de5cd3f81cb5c`;
    axios.get(URL)
      .then(res => {
        const response = res.data.articles;
        this.articles = response;
      })
      .catch(error => {
        console.log(error);
      });
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
