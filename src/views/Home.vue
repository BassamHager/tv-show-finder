<template>
  <main class="home-page">
    <SearchForm />
  </main>
</template>

<script>
import { defineComponent } from "vue";
// components
import SearchForm from "../components/blocks/forms/searchForm/SearchForm.vue";

export default defineComponent({
  name: "Home",
  components: {
    SearchForm,
  },
  setup() {},
});
</script>

<style lang="scss" scoped>
.home-page {
  padding: 2rem 0;
  width: 100%;
  height: 100%;
}
</style>
