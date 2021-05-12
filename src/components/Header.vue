<template>
  <header>
    <a href="javascript:history.go(0)">
      <img src="../assets/img/boolflix-logo.png" alt="boolflix-logo" />
    </a>
    <form class="search">
      <label for="search">Start searching!</label>
      <i class="fas fa-search"></i>
      <input v-model.trim="searchText" type="text" name="search" id="search" />
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
@import "https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.3/css/all.min.css";
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
    @include df("vertical");
    margin-right: 4rem;
    label {
      margin-right: 1rem;
      color: $text-primary;
    }
    i {
      height: 36px;
      width: 50px;
      padding: 10px;
      text-align: center;
      color: $text-secondary;
      background: $text-primary;
      border-top-left-radius: 10px;
      border-bottom-left-radius: 10px;
    }
    input {
      width: 80px;
      padding: 10px;
      outline: none;
      border: transparent;
      text-overflow: ellipsis;
      border-top-right-radius: 10px;
      border-bottom-right-radius: 10px;
      transition: width 0.4s, background 0.4s;
      &:hover,
      &:focus {
        background: #ddd;
        width: 300px;
      }
    }
    button {
      margin-left: 2rem;
      padding: 10px 30px;
      text-transform: uppercase;
      font-weight: bold;
      border-radius: 10px;
      cursor: pointer;
      transition: transform 0.3s;
      &:hover {
        transform: scale(1.14);
      }
    }
  }
}
</style>
