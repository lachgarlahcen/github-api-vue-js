<template>
  <div id="app">
    <Repos />
  </div>
</template>

<script>
import Repos from "./components/Repos.vue";

export default {
  name: "app",
  components: { Repos }
};
</script>

<style>
#app {
  margin: 60px;
}
</style>
