<template>
  <div class="app" id="mapContainer"></div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import "leaflet/dist/leaflet.css";
import L from "leaflet";

export default defineComponent({
  name: "App",
  components: {},
  mounted() {
    let map = L.map("mapContainer").setView([36.06, 103.78], 12);
    const osm = L.tileLayer("http://{s}.tile.osm.org/{z}/{x}/{y}.png", {
      attribution:
        '&copy; <a href="http://osm.org/copyright">OpenStreetMap</a> contributors',
    });
    const esri_streets = L.tileLayer(
      "http://server.arcgisonline.com/ArcGIS/rest/services/World_Street_Map/MapServer/tile/{z}/{y}/{x}"
    );
    const esri_topography = L.tileLayer(
      "http://server.arcgisonline.com/ArcGIS/rest/services/World_Topo_Map/MapServer/tile/{z}/{y}/{x}"
    );

    const imageTile = L.tileLayer(
      "http://10.168.1.223:8002/service/satellite/tile/{z}/{x}/{y}"
    );

   const esri_satellite = L.tileLayer(
      "http://server.arcgisonline.com/ArcGIS/rest/services/World_Imagery/MapServer/tile/{z}/{y}/{x}"
    );

    var baseMaps = {
      OpenStreetMap: osm,
      Streets: esri_streets,
      Topography: esri_topography,
      Satellite: esri_satellite,
    };

    var overlayMaps = {
      Image: imageTile,
    };

    osm.addTo(map);
    imageTile.addTo(map);

    var layerControl = L.control.layers(baseMaps,overlayMaps).addTo(map);

    // layerControl.addBaseLayer(esri_satellite, "Satellite");
    // layerControl.addOverlay(imageTile, "Image");
  },
});
</script>

<style>
#mapContainer {
  width: 100vw;
  height: 100vh;
}
</style>

function mounted() { throw new Error('Function not implemented.'); } function
mounted() { throw new Error('Function not implemented.'); }
