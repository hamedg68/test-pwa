<script setup lang="ts">
import { ref } from "vue";
import installBanner from "./components/InstallBanner.vue";
import reloadPWA from "./components/ReloadPWA.vue";
</script>
<!-- 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 -->
<!-- git add dist -f
git commit -m 'build'
git subtree push --prefix dist origin gh-pages -->
<template>
  <div
    style="
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
    "
  >
    <div style="text-align: center; margin-top: 220px">
      <h1 style="color: indigo">This Is Vue Vite Typescript PWA App</h1>
    </div>
    <img src="./assets/logo.png" width="120" />
    <h1>test offline and reload propmt</h1>
    <h1>test again and again</h1>

    <install-banner></install-banner>
    <reloadPWA></reloadPWA>
  </div>
</template>

<style></style>
