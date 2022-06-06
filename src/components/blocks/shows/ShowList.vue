<template>
  <div class="show-list-wrapper">
    <!-- card -->
    <div
      v-for="{ show } in foundShows"
      :key="show.id"
      @click.prevent="selectShow(show.id)"
      class="show-card"
    >
      <h2 class="show-title">
        {{ show.name }}
      </h2>

      <!--TODO: add a default not found img  -->
      <img
        :src="show.image?.medium || show.image?.original || ''"
        alt="show image"
        class="show-image"
      />
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "ShowList",

  props: {
    foundShows: {
      type: Array,
      required: true,
      default: [],
    },
  },

  setup(props, { emit }) {
    // data

    // methods
    const selectShow = (selectedShowId) => {
      const selected = props.foundShows.find(
        (show) => show.show.id === selectedShowId
      );

      emit("emitSelectedShow", selected.show);
    };

    return {
      selectShow,
    };
  },
});
</script>

<style lang="scss" scoped>
.show-list-wrapper {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  gap: 2rem;
  margin-top: 2rem;

  .show-card {
    background: rgba($color: #000000, $alpha: 0.5);
    border: 1px outset #333;
    cursor: pointer;
    width: min(max(45%, 250px), 100%);
    border-radius: 20px;
    box-shadow: 1px 1px 3px 2px rgba($color: #000000, $alpha: 0.7);

    .show-title {
      color: plum;
      border-radius: 20px;
      text-align: center;
      padding: 1rem;
    }

    .show-image {
      width: 100%;
      border-radius: 20px;
      padding: 1rem;
    }

    &:hover {
      box-shadow: 5px 5px 15px 2px rgba($color: #000000, $alpha: 0.7);
      background: #000;
      transition: 0.5s all ease-in-out;
      border-color: gold;

      .show-title {
        color: gold;
        transition: 1s all ease-in-out;
      }
    }
  }
}
</style>
