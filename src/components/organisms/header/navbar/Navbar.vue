<template>
  <nav :class="isOpen ? '' : 'dynamic-shadow'">
    <!-- main buttons under the main title -->
    <div class="menu">
      <router-link to="/" class="menu-link" @click="toggleMenu(false)">
        <span class="text">Home</span>
      </router-link>

      <router-link to="/about" class="menu-link" @click="toggleMenu(false)">
        <span class="text">About</span>
      </router-link>

      <router-link to="/favorites" class="menu-link" @click="toggleMenu(false)">
        <span class="text">Favorites</span>
      </router-link>
    </div>

    <!-- arrow button opens submenu -->
    <BaseButton
      v-if="!isOpen"
      class="show-submenu-button"
      @click="toggleMenu(true)"
    >
      <span class="material-icons"> keyboard_double_arrow_down </span>
    </BaseButton>

    <!-- toggleable submenu -->
    <div v-else class="submenu">
      <BaseButton class="submenu-button" @click="toggleMenu(false)"
        >settings</BaseButton
      >
      <BaseButton class="submenu-button" @click="toggleMenu(false)"
        >theme</BaseButton
      >
      <BaseButton class="submenu-button" @click="toggleMenu(false)"
        >Close</BaseButton
      >
    </div>
  </nav>
</template>

<script>
import { computed, defineComponent, ref } from "vue";
import BaseButton from "../../../atoms/button/BaseButton.vue";

export default defineComponent({
  name: "Sidebar",
  setup() {
    // data
    const isOpen = ref(false);

    // methods
    const toggleMenu = (open) => {
      isOpen.value = open;

      // toggle body scroll
      toggleBodyScroll();
    };

    const toggleBodyScroll = () => {
      const bodyClasses = document.body.classList;
      isOpen.value
        ? bodyClasses.add("toggleBodyScroll")
        : bodyClasses.remove("toggleBodyScroll");
    };

    return {
      isOpen,

      toggleMenu,
    };
  },
});
</script>

<style lang="scss" scoped>
nav {
  width: 100%;
  height: 5rem;
  overflow: hidden;
  display: grid;
  place-items: center;
  border-radius: 40px;
  transition: 0.6s ease-in-out;

  .menu {
    background: rgba($color: #000000, $alpha: 0.3);
    width: 100%;
    display: flex;
    justify-content: space-around;
    .menu-link {
      padding: 0.5rem;
      color: #bbb;
      text-decoration: none;
      flex-grow: 1;
      display: grid;
      place-items: center;

      &:hover {
        color: #fff;
        text-decoration: underline;
        transition: 0.6s ease-in-out;
        background: rgba($color: #000000, $alpha: 0.6);
      }
    }

    .menu-link:nth-child(2) {
      border-right: 2px solid #666;
      border-left: 2px solid #666;
    }
  }

  .show-submenu-button {
    background: rgba($color: #000000, $alpha: 0.3);
    cursor: pointer;
    width: 100%;
    height: 100%;
    display: grid;
    place-items: center;
    transition: 0.6s ease-in-out;
    color: #bbb;
    border-top: 2px solid #666;

    &:hover {
      color: #fff;
      transition: 0.6s ease-in-out;
      background: rgba($color: #000000, $alpha: 0.6);
    }
  }

  .submenu {
    position: absolute;
    top: 20rem;
    height: 100vh;
    width: min(117rem, 100%);
    padding: 1rem;
    margin: 0 1rem;
    display: flex;
    flex-direction: column;

    background: linear-gradient(90deg, #000851 0%, #1cb5e0 100%);

    .submenu-button {
      display: grid;
      place-items: center;
      margin: 1rem auto 2rem;
      padding: 0.5rem;
      width: min(100%, 40rem);
      cursor: pointer;
      background: rgba($color: #000000, $alpha: 0.3);
      border-radius: 4rem;
      color: #bbb;

      &:hover {
        transition: 0.6s ease-in-out;
        background: plum;
        background: rgba($color: #000000, $alpha: 0.6);
        color: #fff;
      }
    }
  }
}

// for a consistent 3d-like buttons
.dynamic-shadow {
  box-shadow: 5px 4px 5px 0 purple;
}
</style>
