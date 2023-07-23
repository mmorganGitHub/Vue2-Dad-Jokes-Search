<template>
  <div id="mount">
    <NavBar />
    <main>
      <router-view />
    </main>
  </div>
</template>

<script lang="ts">
import NavBar from "@/components/NavBar.vue";

export default {
  name: "App",
  components: {
    NavBar,
  },
};
</script>

<style lang="scss">
@import "./styles/index.scss";
</style>
