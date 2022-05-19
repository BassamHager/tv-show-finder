<template>
  <div class="app">
    <div class="max-viewport">
      <Header class="app-header" />
      <Navbar />
    </div>

    <main class="main max-viewport">
      <router-view />
    </main>

    <!-- footer  -->
  </div>
</template>

<script>
import { defineComponent } from "vue";
// components
import Header from "./components/organisms/header/Header.vue";
import Navbar from "./components/organisms/header/navbar/Navbar.vue";

export default defineComponent({
  components: {
    Header,
    Navbar,
  },
  setup() {
    return {};
  },
});
</script>
<style lang="scss">
:root {
  --main-color: purple;
  --secondary-color: plum;
  --dark-color: #000851;
  --light-color: #1cb5e0;
  --lg-width: 1200px;
  --main-bg: #1d6d86;
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: helvetica, sans-serif;
}

html {
  font-size: 62.5%;
}

body {
  margin: 0;
  font-size: 1.6rem;
}

.app {
  background: linear-gradient(90deg, #000851 0%, #1cb5e0 100%);
  height: 100vh;
  padding: 0 1rem;

  .main {
    padding: 1rem;
  }

  // restrict larger screens
  .max-viewport {
    max-width: 117rem;
    margin: 0 auto;
  }
}
</style>
