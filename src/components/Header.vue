<template>
  <header>
    <a href="#">
      <img src="../assets/img/boolflix-logo.png" alt="boolflix-logo" />
    </a>
    <form class="search">
      <label for="search">Start searching!</label>
      <input
        v-model.trim="searchText"
        type="text"
        name="search"
        id="search"
        placeholder="Search your favourite movies or TV shows!"
      />
      <button type="submit" @click.prevent="$emit('searchText', searchText)">
        Go!
      </button>
    </form>
  </header>
</template>

<script>
export default {
  name: "Header",
  data() {
    return {
      searchText: "",
    };
  },
};
</script>

<style scoped lang="scss">
@import "../styles/mixins";
@import "../styles/vars";

header {
  @include df("vertical");
  justify-content: space-between;
  position: fixed;
  z-index: 2;
  width: 100%;
  height: 90px;
  background: $brand-color;

  form {
    margin-right: 4rem;
    label {
      margin-right: 1rem;
      color: $text-primary;
    }
    input {
      width: 300px;
      padding: 10px;
      border-radius: 10px;
    }
    button {
      margin-left: 2rem;
      padding: 10px 30px;
      border-radius: 10px;
      cursor: pointer;
    }
  }
}
</style>
