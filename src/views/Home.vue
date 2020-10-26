<template>
  <div class="home">
    <div id="map"></div>
  </div>
</template>

<style>
#map {
  width: 100%;
  height: 800px;
}
</style>

<script>
import mapboxgl from "mapbox-gl";
export default {
  data: function() {
    return {
      message: "Welcome to Vue.js!",
    };
  },
  mounted: function() {
    mapboxgl.accessToken = "<your-access-token>";
    const map = new mapboxgl.Map({
      container: "map",
      style: "mapbox://styles/mapbox/streets-v11", // stylesheet location
      center: [-122.431297, 37.773972], // starting position [lng, lat]
      zoom: 12, // starting zoom
    });
  },
  methods: {},
};
</script>
