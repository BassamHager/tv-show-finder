<template>
  <div class="show-list-wrapper">
    <ShowCard :shows="foundShows" :selectShow="selectShow" />
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
// components
import ShowCard from "../card/ShowCard.vue";

export default defineComponent({
  name: "ShowList",

  components: {
    ShowCard,
  },

  props: {
    foundShows: {
      type: Array,
      required: true,
      default: [],
    },
    selectShow: {
      type: Function,
      required: true,
      default: () => {},
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
}
</style>
