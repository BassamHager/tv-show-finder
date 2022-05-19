<template>
  <header>
    <router-link to="/" class="app-title">
      <img src="../../../assets/tv-show.jpg" alt="app logo" />
      <h1>tv <span>show</span> find<span>er</span></h1>
    </router-link>
  </header>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "Header",
  setup() {},
});
</script>

<style lang="scss" scoped>
header {
  height: 15rem;
  display: grid;
  place-items: center;
  text-transform: uppercase;
  letter-spacing: 2px;

  .app-title {
    display: flex;
    justify-content: center;
    align-items: center;
    max-width: var(--lg-width);
    padding: 0 1rem;
    text-align: center;
    color: #fff;
    text-shadow: 3px 1px 3px purple;
    text-decoration: none;

    img {
      object-fit: stretch;
      display: block;
      width: 75px;
      margin-right: 2rem;
      border-radius: 50%;
      box-shadow: 5px 4px 10px 0 purple;
    }

    h1 {
      span {
        text-shadow: 3.5px 7px 5px purple;
      }
    }
  }
}
</style>
