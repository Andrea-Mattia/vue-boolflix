<template>
  <main>
    <section class="container">
      <Card v-for="item in content" :key="item.id" :info="item" />
    </section>
  </main>
</template>

<script>
import Card from "../components/Card.vue";

export default {
  name: "MainContent",
  components: {
    Card,
  },
  props: ["content"],
};
</script>

<style scoped lang="scss">
@import "../styles/mixins";
@import "../styles/vars";

main {
  min-height: 100vh;
  padding-top: 120px;
  background: $brand-background;
  color: $text-primary;
  section {
    @include df("horizontal");
    flex-wrap: wrap;
  }
}
</style>
