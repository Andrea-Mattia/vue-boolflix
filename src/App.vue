<template>
  <div id="app">
    <Header @searchText="getFilmTV" />
    <MainContent :content="filmList.concat(seriesList)" />
  </div>
</template>

<script>
import axios from "axios";
import Header from "./components/Header.vue";
import MainContent from "./components/MainContent.vue";

export default {
  name: "App",
  components: {
    Header,
    MainContent,
  },
  data() {
    return {
      apiFilmURL: "https://api.themoviedb.org/3/search/movie",
      apiSeriesURL: "https://api.themoviedb.org/3/search/tv",
      apiTrendingURL: "https://api.themoviedb.org/3/trending/all/week",
      apiKey: "2789b3e89104d5b01e7ea9ac095a6e01",
      filmList: [],
      seriesList: [],
    };
  },
  created() {
    axios
      .get(this.apiTrendingURL, {
        params: {
          api_key: this.apiKey,
          language: "it-IT",
        },
      })
      .then((res) => {
        this.filmList = res.data.results;
      })
      .catch((err) => {
        console.log("ERROR", err);
      });
  },
  methods: {
    getFilmTV(searchText) {
      if (searchText !== "") {
        const apiParams = {
          api_key: this.apiKey,
          language: "it-IT",
          query: searchText,
        };
        axios
          .get(this.apiFilmURL, {
            params: apiParams,
          })
          .then((res) => {
            this.filmList = res.data.results;
          })
          .catch((err) => {
            console.log("ERROR", err);
          });
        axios
          .get(this.apiSeriesURL, {
            params: apiParams,
          })
          .then((res) => {
            this.seriesList = res.data.results;
          })
          .catch((err) => {
            console.log("ERROR", err);
          });
      }
    },
  },
};
</script>

<style lang="scss">
@import "./styles/general";
@import "./styles/utilities";
</style>
