<template>
  <div class="geolocation">
    <h2>Geolocation</h2>
    <input type="text" v-model="address" /><button
      v-on:click="geolocateAddress()"
    >
      See this!
    </button>
    <div id="map"></div>
  </div>
</template>

<style>
#map {
  width: 100%;
  height: 1000px;
}
</style>

<script>
import mapboxgl from "mapbox-gl";
export default {
  data: function() {
    return {
      address: "San Francisco",
    };
  },
  mounted: function() {
    this.geolocateAddress();
  },
  methods: {
    geolocateAddress: function() {
      mapboxgl.accessToken = process.env.VUE_APP_MAPBOX_ACCESS_TOKEN;
      var mapboxClient = mapboxSdk({ accessToken: mapboxgl.accessToken });
      mapboxClient.geocoding
        .forwardGeocode({
          query: this.address,
          autocomplete: false,
          limit: 1,
        })
        .send()
        .then(function(response) {
          if (
            response &&
            response.body &&
            response.body.features &&
            response.body.features.length
          ) {
            var feature = response.body.features[0];

            var map = new mapboxgl.Map({
              container: "map",
              style: "mapbox://styles/mapbox/streets-v11",
              center: feature.center,
              zoom: 10,
            });
            new mapboxgl.Marker().setLngLat(feature.center).addTo(map);
          }
        });
    },
  },
};
</script>
