<template>
  <div
    v-for="{ show } in shows"
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
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "Card",
  props: {
    shows: {
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
  setup() {},
});
</script>

<style lang="scss" scoped>
.show-card {
  background: rgba($color: #000000, $alpha: 0.5);
  border: 1px outset #333;
  cursor: pointer;
  width: min(max(29%, 300px), 100%);
  border-radius: 20px;
  box-shadow: 3px 3px 5px 3px rgba($color: #000000, $alpha: 0.7);

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
    box-shadow: none;
    background: rgba($color: #000000, $alpha: 0.3);
    transition: 0.5s all ease-in-out;

    .show-title {
      color: gold;
      transition: 1s all ease-in-out;
    }
  }
}
</style>
