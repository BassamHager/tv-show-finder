<template>
  <form class="search-form" @submit.prevent="submitSearch">
    <input
      id="search-input"
      type="text"
      placeholder="Search a TV show..."
      v-model="searchTerm"
    />
    <input type="submit" value="Search" />
  </form>
</template>

<script>
import { defineComponent, onMounted, ref } from "vue";
// components
import SearchBar from "../../searchBar/SearchBar.vue";

export default defineComponent({
  name: "SearchForm",
  components: {
    SearchBar,
  },
  setup() {
    // data
    const searchTerm = ref("");

    // methods
    const submitSearch = () => {
      console.log("term:::", searchTerm.value);
    };

    onMounted(() => {
      const searchInput = document.querySelector("#search-input");
      searchInput.focus();
    });

    return {
      searchTerm,

      submitSearch,
    };
  },
});
</script>

<style lang="scss" scoped>
.search-form {
  display: grid;
  place-items: center;

  input[type="text"] {
    width: min(100%, 80rem);
    padding: 1rem;
    border-radius: 5rem;
    border: none;
    margin-bottom: 2rem;
    font-size: 2rem;

    &:focus {
      outline: none;
    }
  }

  input[type="submit"] {
    border-radius: 50rem;
    width: min(100%, 80rem);
    padding: 1rem;
    border: none;
    box-shadow: 1px 1px 3px 1px purple;
    background: rgba($color: #000000, $alpha: 0.5);
    color: #bbb;
    cursor: pointer;

    &:hover {
      box-shadow: 2px 1px 3px 1px purple;
      transition: 0.3s ease-in-out;
      background: rgba($color: #000000, $alpha: 0.6);
      color: #fff;
    }
  }
}
</style>
