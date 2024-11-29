<template>
  <RouterView />
</template>

<script setup lang="ts">
import { RouterView } from 'vue-router';
</script>

<style lang="scss">
html {
  font-family: Inter, sans-serif;
  font-size: 14px;
}

body {
  overflow: hidden;
  height: 100vh;
}

#app {
  overflow: auto;
  max-width: 1280px;
  height: 100%;
  margin: 0 auto;
  background: white;
}
</style>
