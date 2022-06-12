<template>
  <div class="auto-fetched-shows-wrapper">
    <div
      v-for="[genreName, genreArray] in showsPerGenre"
      :key="genreName"
      class="auto-fetched-shows"
    >
      <!-- genre name -->
      <h2 v-if="genreArray.length" class="genre-name">{{ genreName }}</h2>

      <!-- shows per genre -->
      <div class="shows-per-genre-wrap">
        <ShowCard
          v-for="{ show } in genreArray"
          :show="show"
          :source="'autoFetch'"
        />
      </div>
    </div>
    <button @click="fetchShows">fetch</button>
    <button @click="filterGenres">filter</button>
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive, ref } from "vue";
// mocked
import mockedFullData from "../../../mock/fullData.json";
import ShowCard from "../card/ShowCard.vue";

export default defineComponent({
  components: { ShowCard },
  name: "AutoFetchedShowList",

  props: {
    selectShow: {
      type: Function,
      required: true,
      default: () => {},
    },
    source: {
      type: String,
      required: false,
      default: "",
    },
  },

  setup() {
    // data
    const autoFetchedShows = ref([]);
    let showsPerGenre = ref(new Map());

    // methods
    const fetchShows = async () => {
      try {
        // fetch shows
        // const fetchedShows = await fetch();
        // `${import.meta.env.VITE_AUTO_FETCH_SHOWS_URL}`
        // parse to json
        // const parsedShows = await fetchedShows.json();
        // update state
        // autoFetchedShows.value = parsedShows;
        autoFetchedShows.value = mockedFullData;

        console.log("auto:::", autoFetchedShows.value);
      } catch (error) {
        console.error("fetchShows:::", error);
      }
    };

    const filterGenres = () => {
      const genreMap = new Map();

      autoFetchedShows.value.forEach((show) => {
        show.show?.genres.forEach((genre) => {
          genreMap.has(genre)
            ? genreMap.get(genre).push(show)
            : genreMap.set(genre, [show]);
        });
      });

      const sortedGenres = new Map(
        [...genreMap].sort((a, b) => {
          a[1].length - b[1].length;
        })
      );

      // update state
      showsPerGenre.value = sortedGenres;

      console.log("state:::", showsPerGenre);
    };

    return {
      showsPerGenre,

      fetchShows,
      filterGenres,
    };
  },
});
</script>

<style lang="scss" scoped>
.auto-fetched-shows-wrapper {
  margin-top: 4rem;
  color: chocolate;

  .genre-name {
    color: #fff;
    text-transform: uppercase;
    text-align: center;
    background: rgba($color: #000, $alpha: 0.5);
    padding: 2rem;
    border-bottom: 1px solid #000;
  }

  .shows-per-genre-wrap {
    background: rgba($color: #000, $alpha: 0.4);
    padding: 2rem 0;
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
    gap: 2rem;
  }
}
button {
  width: 100%;
  padding: 2rem;
  background: rgba($color: #000000, $alpha: 0.5);
  color: #fff;
  font-size: 2rem;
}
</style>
