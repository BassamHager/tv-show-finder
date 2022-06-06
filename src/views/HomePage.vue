<template>
  <main class="home-page">
    <SearchForm @emitSearchTerm="searchShows" />

    <!-- searched & found shows -->
    <ShowList
      v-if="!isSelectedShow"
      :foundShows="foundShows"
      @emitSelectedShow="selectShow"
    />

    <!-- clicked show details -->
    <ShowDetailsPage
      v-else
      :showDetails="selectedShow"
      :isSelectedShow="isSelectedShow"
      @emitBack="backToHome"
      :backToHome="backToHome"
    />
  </main>
</template>

<script>
import { computed, defineComponent, ref } from "vue";
// components
import SearchForm from "../components/blocks/forms/searchForm/SearchForm.vue";
import ShowList from "../components/blocks/shows/ShowList.vue";
import ShowDetailsPage from "./ShowDetailsPage.vue";

export default defineComponent({
  name: "Home",
  components: {
    SearchForm,
    ShowList,
    ShowDetailsPage,
  },

  props: {
    foundShows: {
      type: Array,
      required: true,
      default: [],
    },
    showDetails: {
      type: Object,
      required: true,
      default: {},
    },
    backToHome: {
      type: Function,
      required: true,
      default: () => {},
    },
  },

  setup() {
    // data
    const foundShows = ref([]);
    const selectedShow = ref({});
    const isSelectedShow = ref(false);

    // methods
    const searchShows = async (searchTerm) => {
      try {
        // fetch by term
        const fetchedShows = await fetch(
          `${import.meta.env.VITE_SEARCH_SHOWS_URL}${searchTerm}`
        );
        // parse data
        const parsedShows = await fetchedShows.json();
        // update state
        if (parsedShows?.length) foundShows.value = parsedShows;

        isSelectedShow.value = false;
      } catch (error) {
        console.error("searchShows:::", error);
      }
    };

    const selectShow = (show) => {
      selectedShow.value = show;
      isSelectedShow.value = true;
    };

    const backToHome = () => (isSelectedShow.value = false);

    return {
      foundShows, // [{}]
      selectedShow, // {}
      isSelectedShow, // click a show-card => true

      searchShows, // fetch shows by term => foundShows
      selectShow, // assign show object => selectedShow
      backToHome, // click back button => isSelectedShow = false
    };
  },
});
</script>

<style lang="scss" scoped>
.home-page {
  padding: 2rem 0;
  width: 100%;
  height: 100%;
}
</style>
