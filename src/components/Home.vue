<template>
  <div class="container">
    <div class="row">
      <div class="articles-container">
        <div
          v-for="(article, index) in articles"
          :key="index"
          class="card col-md-6"
        >
          <img
            v-if="article.urlToImage !== null"
            :src="article.urlToImage"
            class="card-img-top"
            alt="Image not available"
          />
          <img
            v-else
            src="https://images.pexels.com/photos/159652/table-food-book-newspaper-159652.jpeg"
            class="card-img-top"
            alt="Image not available"
          />
          <div class="card-body">
            <h5 class="card-title">{{ article.title }}</h5>
            <p class="card-text">
              <b>Description:</b> {{ article.description }}
            </p>
            <p v-if="article.author !== null" class="card-text">
              <b>Author:</b> {{ article.author }}
            </p>
            <p v-else class="card-text">
              <b>Author:</b> Author name not available
            </p>
            <p class="card-text">
              <b>Date Published:</b> {{ formatTime(article.publishedAt) }}
            </p>
            <a :href="article.url" target="blank" class="btn btn-primary"
              >Read News</a
            >
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "Home",
  data() {
    return {
      articles: []
    };
  },
  methods: {
    formatTime(time) {
      let newTime = time.split("T");
      return newTime[0];
    }
  },
  mounted() {
    const URL = `https://newsapi.org/v2/top-headlines?country=ng&apiKey=ee85542cb07b4ad3997de5cd3f81cb5c`;
    axios
      .get(URL)
      .then(res => {
        const response = res.data.articles;
        this.articles = response;
        // console.log(this.articles);
      })
      .catch(error => {
        console.log(error);
      });
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.card {
  margin: 20px;
  width: 600px;
}
.articles-container {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  justify-items: center;
}

@media only screen and (max-width: 1000px) {
  .articles-container {
    margin: 10px;
    grid-template-columns: repeat(1, 1fr);
  }
}
</style>
