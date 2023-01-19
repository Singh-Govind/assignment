<template>
  <div>
    <div id="input">
      Please select a GeoJson file:
      <input type="file" @change="getGeoJsonData" />
      <button @click="submitFile">Submit</button>
    </div>
    <LeafMap :data="{ cords, polygonData, geojsonData }" :isData="isData" />
  </div>
</template>

<script>
import LeafMap from "./components/LeafMap.vue";
export default {
  name: "App",
  components: {
    LeafMap,
  },
  data() {
    return {
      polygonData: [],
      geojsonData: [],
      cords: [],
      isData: false,
    };
  },
  methods: {
    getGeoJsonData(event) {
      this.isData = false;
      this.isgeojsonData = [];
      this.cords = [];
      this.polygonData = [];

      var file = event.target.files[0];
      if (!file) {
        alert("please select a file");
        return;
      }
      var reader = new FileReader();

      reader.onload = (e) => {
        var content = reader.result;
        let temp = JSON.parse(content);
        let temp2 = JSON.parse(content);
        this.geojsonData = temp2;
        this.polygonData = temp.features[0].geometry.coordinates[0];
        this.cords = temp.features[0].geometry.coordinates[0][0];
      };

      reader.readAsText(file);
      console.log(this.geojsonData);
    },
    submitFile() {
      if (this.cords.length !== 0) {
        this.isData = true;
      } else {
        alert("please select a file");
      }
    },
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
