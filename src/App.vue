<template>
  <div>
    <GeoJson />
  </div>
</template>

<script>
import GeoJson from "./components/GeoJson.vue";
export default {
  name: "App",
  components: {
    GeoJson,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
