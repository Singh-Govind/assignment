<template>
  <div id="input">
    Please select a GeoJson file:
    <input type="file" @change="handleFileChange" />
    <button @click="submit">Submit</button>
    {{ isData ? "True" : "False" }}
  </div>
  <div id="map" style="height: 600px; width: 800px">
    <l-map ref="map" v-model:zoom="zoom" :center="[47.41322, -1.219482]">
      <l-tile-layer
        url="https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png"
        layer-type="base"
        name="OpenStreetMap"
      ></l-tile-layer>
      <l-polygon
        v-if="isData"
        :lat-lngs="getData(polygon.latlngs)"
        :center="getCenter(center)"
        color="red"
      ></l-polygon>
    </l-map>
  </div>
</template>

<script>
import "leaflet/dist/leaflet.css";
import { isProxy, toRaw } from "vue";
import {
  LMap,
  LTileLayer,
  LPolygon,
  LPolyline,
  LGeoJson,
} from "@vue-leaflet/vue-leaflet";

export default {
  components: {
    LMap,
    LTileLayer,
    LPolyline,
    LPolygon,
    LGeoJson,
  },
  data() {
    return {
      isData: false,
      zoom: 3,
      center: [47.31322, -1.319482],
      polygon: {
        latlngs: [
          [47.2263299, -1.6222],
          [47.21024000000001, -1.6270065],
          [47.1969447, -1.6136169],
          [47.18527929999999, -1.6143036],
          [47.1794457, -1.6098404],
          [47.1775788, -1.5985107],
          [47.1676598, -1.5753365],
          [47.1593731, -1.5521622],
          [47.1593731, -1.5319061],
          [47.1722111, -1.5143967],
          [47.1960115, -1.4841843],
          [47.2095404, -1.4848709],
          [47.2291277, -1.4683914],
          [47.2533687, -1.5116501],
          [47.2577961, -1.5531921],
          [47.26828069, -1.5621185],
          [47.2657179, -1.589241],
          [47.2589612, -1.6204834],
          [47.237287, -1.6266632],
          [47.2263299, -1.6222],
        ],
        color: "green",
      },
      geojson: {},
    };
  },
  methods: {
    handleFileChange(event) {
      this.isData = false;
      var file = event.target.files[0];
      var reader = new FileReader();

      reader.onload = (e) => {
        var content = reader.result;
        let temp = JSON.parse(content);
        let temp2 = JSON.parse(content);
        this.geojson = temp2;
        this.polygon.latlngs = temp.features[0].geometry.coordinates[0];
        this.center = temp.features[0].geometry.coordinates[0][0];
        // console.log(this.polygon.latlngs);
      };

      reader.readAsText(file);
    },
    submit() {
      // console.log(this.polygon.latlngs);

      // this.polygon.latlngs = rawData;
      this.isData = true;
    },
    getData(data) {
      let rawData = data;

      if (isProxy(data)) {
        rawData = toRaw(data);
      }
      console.log(rawData);
      return rawData;
    },
    getCenter(data) {
      let rawData = data;

      if (isProxy(data)) {
        rawData = toRaw(data);
      }
      console.log(rawData);
      return rawData;
    },
  },
};
</script>

<style scoped>
#input {
  margin: 2rem 1rem;
}
#map {
  display: flex;
  justify-content: center;
  margin: auto;
}
</style>
