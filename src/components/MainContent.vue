<template>
  <section>
    <header>
      <img src="../assets/img/boolflix-logo.png" alt="boolflix-logo" />
      <form class="search">
        <label for="search">Start searching movies!</label>
        <input
          v-model="searchFilm"
          type="text"
          name="search"
          id="search"
          placeholder="Type here!"
        />
        <button type="submit" @click.prevent="getFilm">GO!</button>
      </form>
    </header>

    <main>
      <section class="container">
        <ul v-for="film in filmList" :key="film.id">
          <li>Titolo: {{ film.title }}</li>
          <li>Titolo Originale: {{ film.original_title }}</li>
          <li>Voto: {{ film.vote_average }}</li>
          <li>Lingua: {{ film.original_language }}</li>
        </ul>
      </section>
    </main>
  </section>
</template>

<script>
import axios from "axios";

export default {
  name: "MainContent",
  data() {
    return {
      apiURL:
        "https://api.themoviedb.org/3/search/movie?api_key=2789b3e89104d5b01e7ea9ac095a6e01&language=it-IT",
      filmList: [],
      searchFilm: "",
    };
  },
  methods: {
    getFilm() {
      axios
        .get(this.apiURL, {
          params: {
            query: this.searchFilm,
          },
        })
        .then((res) => {
          this.filmList = res.data.results;
          this.searchFilm = "";
        })
        .catch((err) => {
          console.log("ERROR", err);
        });
    },
  },
};
</script>

<style scoped lang="scss">
@import "../styles/mixins";
@import "../styles/vars";

header {
  @include df("vertical");
  justify-content: space-between;
  height: 90px;
  background: $brand-color;
  form {
    margin-right: 4rem;
    label {
      margin-right: 1rem;
      color: $text-primary;
    }
    input {
      padding: 10px;
      border-radius: 10px;
      margin-right: 2rem;
    }
    button {
      padding: 10px 30px;
      border-radius: 10px;
      cursor: pointer;
    }
  }
}

main {
  height: calc(100vh - 90px);
  padding: 2rem;
  background: $brand-background;
  color: $text-primary;
  ul {
    margin-bottom: 2rem;
  }
}
</style>
