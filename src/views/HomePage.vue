<template>
  <main class="home-page">
    <SearchForm @emitSearchTerm="searchShows" />

    <!-- auto fetched showList -->
    <AutoFetchedShowList
      :selectShow="selectShow"
      @emitClickedShowCardId="getClickedShowCardId"
    />

    <!-- searched & found showList -->
    <FoundShowList
      v-if="!isSelectedShow"
      :foundShows="foundShows"
      @emitSelectedShow="selectShow"
    />

    <!-- clicked show details -->
    <ShowDetails
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
import AutoFetchedShowList from "../components/blocks/shows/AutoFetchedShowList.vue";
import FoundShowList from "../components/blocks/shows/FoundShowList.vue";
import ShowDetails from "../components/blocks/shows/ShowDetails.vue";

export default defineComponent({
  name: "Home",
  components: {
    SearchForm,
    AutoFetchedShowList,
    FoundShowList,
    ShowDetails,
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
    selectShow: {
      type: Function,
      required: true,
      default: () => {},
    },
  },

  setup(_, { emit }) {
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

    // const selectShow = (show) => {
    //   selectedShow.value = show;
    //   isSelectedShow.value = true;
    // };

    const getClickedShowCardId = (clickedShowId, source) => {
      if (source === "autoFetch") {
        const selected = shows.find((show) => show.show.id === clickedShowId);
      }
    };

    const selectShow = (shows, clickedShowId) => {
      const selected = shows.find((show) => show.show.id === clickedShowId);

      emit("emitSelectedShow", selected.show);
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
