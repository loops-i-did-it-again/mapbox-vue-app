<template>
  <div class="home">
    <div id="map"></div>
  </div>
</template>

<style>
#map {
  width: 100%;
  height: 1000px;
}
#marker {
  background-image: url("https://image.flaticon.com/icons/png/512/184/184549.png");
  background-size: cover;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  cursor: pointer;
}

.mapboxgl-popup {
  max-width: 200px;
}
</style>

<script>
import mapboxgl from "mapbox-gl";
export default {
  data: function() {
    return {
      places: [
        {
          long: -122.4211,
          lat: 37.79193,
          description: "Bob's donuts!",
        },
        {
          long: -122.42497,
          lat: 37.77858,
          description: "Johnny's Donuts!",
        },
        {
          long: -122.02575,
          lat: 36.9738,
          description: "Marini's Downtown Santa Cruz",
        },
        {
          long: -122.03712,
          lat: 37.97473,
          description: "Alpine bakery, Concord!",
        },
      ],
    };
  },
  mounted: function() {
    mapboxgl.accessToken = process.env.VUE_APP_MAPBOX_ACCESS_TOKEN;
    const map = new mapboxgl.Map({
      container: "map",
      style: "mapbox://styles/mapbox/light-v10", // stylesheet location
      center: [-122.431297, 37.773972], // starting position [lng, lat]
      zoom: 9, // starting zoom
    });

    this.places.forEach((place) => {
      var popup = new mapboxgl.Popup({ offset: 25 }).setText(place.description);
      // create DOM element for the marker
      var el = document.createElement("div");
      el.id = "marker";
      // create the marker
      new mapboxgl.Marker(el)
        .setLngLat([place.long, place.lat])
        .setPopup(popup) // sets a popup on this marker
        .addTo(map);
    });
  },
  methods: {},
};
</script>
