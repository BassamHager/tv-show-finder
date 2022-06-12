<template>
  <div class="show-details">
    <!-- show title -->
    <h2 class="show-details-title">{{ showDetails.name }}</h2>

    <!-- show image -->
    <img
      :src="showDetails.image?.medium || ''"
      alt="show image"
      class="show-details-image"
    />

    <!-- show genres -->
    <div class="show-details-genres">
      <h4 v-for="genre in showDetails.genres" :key="genre">
        {{ genre }}
      </h4>
    </div>

    <!-- show description -->
    <div v-html="showDetails?.summary" class="show-details-description"></div>

    <!-- go back button -->
    <BaseButton @click="backToHome" class="show-details-button-back">
      Back
    </BaseButton>
  </div>
</template>

<script lang="ts">
import { defineComponent, onMounted, onUnmounted, ref } from "vue";
import { useRoute } from "vue-router";
// components
import BaseButton from "../../atoms/button/BaseButton.vue";

export default defineComponent({
  name: "ShowDetails",

  components: {
    BaseButton,
  },

  props: {
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

  setup(_, { emit }) {
    const goBack = () => {
      console.log("go back");
      emit("emitBack");
    };

    return {
      goBack,
    };
  },
});
</script>

<style lang="scss" scoped>
.show-details {
  display: flex;
  flex-wrap: wrap;
  width: 100%;

  .show-details-title {
    color: #fff;
    width: 100%;
    text-align: center;
    padding: 2rem 1rem;
    letter-spacing: 1.5px;
  }

  .show-details-image {
    border-radius: 4px;
    margin: auto;
  }

  .show-details-genres {
    flex-grow: 1;
    display: flex;
    justify-content: start;

    & * {
      color: plum;
      margin-left: 1rem;
      padding: 1rem;
    }
  }

  .show-details-description {
    background: rgba($color: #000000, $alpha: 0.5);
    padding: 1rem;
    color: #bbb;
    text-align: justify;
    line-height: 2.5rem;
    border-radius: 4px;
    margin-top: 1rem;

    &:deep(b),
    :deep(i) {
      color: plum;
    }
  }

  .show-details-button-back {
    width: 100%;
    padding: 1rem;
    text-transform: uppercase;
    color: #bbb;
    background: rgba($color: #000000, $alpha: 0.3);
    border-radius: 50px;
    box-shadow: 1px 1px 3px 1px purple;
    border: none;
    margin-top: 1rem;

    &:hover {
      background: rgba($color: #000000, $alpha: 0.6);
      // transition: all 0.3s ease-in-out;
    }
  }
}
</style>
