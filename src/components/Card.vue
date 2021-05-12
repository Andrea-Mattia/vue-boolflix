<template>
  <div class="card">
    <img
      class="poster"
      :src="`https://image.tmdb.org/t/p/w342/${info.poster_path}`"
      :alt="info.title"
      v-if="info.poster_path != null"
    />
    <img
      class="poster"
      src="https://upload.wikimedia.org/wikipedia/commons/a/ac/No_image_available.svg"
      alt="no-img-found"
      v-else
    />
    <ul>
      <li>
        <strong>Titolo: </strong>
        {{ info.title == null ? info.name : info.title }}
      </li>
      <li
        v-if="
          info.original_title != info.title || info.original_name != info.name
        "
      >
        <strong>Titolo Originale: </strong>
        {{
          info.original_title == null ? info.original_name : info.original_title
        }}
      </li>
      <li>
        <strong>Voto: </strong>
        <span
          v-for="(star, index) in Math.ceil(info.vote_average / 2)"
          :key="index"
        >
          <i class="fas fa-star"></i
        ></span>
        <span
          v-for="(star, index) in 5 - Math.ceil(info.vote_average / 2)"
          :key="'A' + index"
        >
          <i class="far fa-star"></i
        ></span>
      </li>
      <li>
        <strong>Lingua: </strong>
        <span v-if="info.original_language === 'it'">
          <img src="../assets/img/it.png" alt="it-flag" />
        </span>
        <span v-else-if="info.original_language === 'en'">
          <img src="../assets/img/en.png" alt="en-flag" />
        </span>
        <span v-else>
          {{ info.original_language }}
        </span>
      </li>
      <li>
        <strong>Data di uscita: </strong>
        {{
          info.release_date == null ? info.first_air_date : info.release_date
        }}
      </li>
      <li class="overview">
        <strong>Overview: </strong>
        {{ info.overview }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "Card",
  props: ["info"],
};
</script>

<style scoped lang="scss">
@import "https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.3/css/all.min.css";
@import "../styles/vars";

.card {
  position: relative;
  width: 340px;
  height: 500px;
  margin-right: 20px;
  margin-bottom: 20px;
  overflow: hidden;
  cursor: pointer;
  transition: transform 0.2s;
  &::after {
    content: "";
    position: absolute;
    top: 0;
    left: 0;
    height: 100%;
    width: 100%;
    background-color: rgba(#000, 0.8);
    opacity: 0;
    transition: opacity 0.2s;
  }
  &:hover {
    transform: scale(1.12);
    z-index: 1;
  }
  &:hover::after,
  &:hover ul {
    opacity: 1;
  }
  &:hover ul {
    bottom: 1rem;
  }
  .poster {
    position: absolute;
    top: 0;
    left: 0;
    object-fit: contain;
  }
  ul {
    z-index: 1;
    position: absolute;
    bottom: 100%;
    left: 1rem;
    right: 1rem;
    list-style: none;
    color: $text-primary;
    opacity: 0;
    transition: opacity 0.2s, bottom 0.2s;
    li {
      margin-bottom: 1rem;
      &.overview {
        max-height: 200px;
        overflow-y: auto;
      }
    }
  }
  span {
    margin-left: 5px;
    img {
      height: 15px;
    }
  }
}
</style>
