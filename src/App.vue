<script setup lang="ts">
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
    <install-banner style="margin-top: 120px;"></install-banner>
    <reloadPWA></reloadPWA>

    <div style="text-align: center;"><h1 style="color: indigo;">This Is Vue Vite Typescript PWA App</h1></div>
    <img src="./assets/logo.png" width="120" />
    <h1>test offline and reload propmt</h1>
    <h1>test again</h1>
  </div>
</template>

<style></style>
