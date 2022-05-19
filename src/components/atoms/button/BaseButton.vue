<template>
  <button
    :id="id"
    :type="type"
    class="base-button"
    :class="[{ 'w-full': !!block, reversed: !!reversed }, interactionClass]"
    :disabled="disabled"
    @click="$emit('click')"
  >
    <slot />
  </button>
</template>

<script>
import { computed, defineComponent } from "vue";

export default defineComponent({
  props: {
    id: {
      type: String,
      required: false,
      default: "",
    },
    type: {
      type: String,
      required: false,
      default: "button",
    },
    disabled: {
      type: Boolean,
      required: false,
      default: false,
    },
    block: {
      type: Boolean,
      required: false,
      default: false,
    },
    reversed: {
      type: Boolean,
      required: false,
      default: false,
    },
  },

  emits: ["click"],

  setup(props) {
    const interactionClass = computed(() =>
      props.reversed ? "secondary-button-bg" : "main-button-bg"
    );

    return {
      interactionClass,
    };
  },
});
</script>

<style lang="scss" scoped>
button.base-button {
  cursor: pointer;
  padding: 5px;

  &:focus {
    outline: none;
  }
}

.main-button-bg {
  background: var(--dark-color);
}

.secondary-button-bg {
  background: var(--light-color);
}
</style>
