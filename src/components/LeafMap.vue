<template>
  <!-- <button @click="printData">click</button> -->
  <div id="map"></div>
</template>

<script>
import leaflet from "leaflet";
import { onMounted, onUpdated } from "vue";
export default {
  name: "LeafMap",
  components: {},
  props: ["data", "isData"],
  setup(props) {
    let map;
    onMounted(() => {
      map = leaflet.map("map").setView([51.505, -0.09], 10);

      // add tile layer
      leaflet
        .tileLayer("https://tile.openstreetmap.org/{z}/{x}/{y}.png", {
          maxZoom: 19,
          attribution:
            '&copy; <a href="http://www.openstreetmap.org/copyright">OpenStreetMap</a>',
        })
        .addTo(map);
    });

    const updateMap = () => {
      let j = leaflet
        .geoJSON(props.data.geojsonData, {
          style: () => {
            return {
              color: "blue",
            };
          },
        })
        .addTo(map);

      map.fitBounds(j.getBounds(), 8);
    };

    onUpdated(() => {
      if (props.isData) {
        updateMap();
      }
    });

    return { updateMap };
  },
};
</script>

<style scoped>
#map {
  height: 75vh;
  max-width: 80vw;
  margin: auto;
  margin-top: 2rem;
}
</style>
