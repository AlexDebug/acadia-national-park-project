<template>
    <div id="container">
        <div id="mapContainer" class="hidden_from_view"></div>  
    </div>
</template>

<script>
// import content from "./../assets/data.json"
import L from "leaflet"
import "leaflet/dist/leaflet.css";
import features from "./../assets/features.json"
import geoIcon from "./../assets/icons/rocks.png"
import hidroIcon from "./../assets/icons/water.png"
import atmoIcon from "./../assets/icons/wind(1).png"
import bioIcon from "./../assets/icons/trunk.png"

export default {
  name: "MainMap",
  emits: ["FeatureClicked"],
  methods: {
    setuptMap: function () {
      let mapDiv = L.map("mapContainer", {minZoom:11, zoomControl: false}).setView([44.3386, -68.2908441], 11);
      console.log(mapDiv);
      L.tileLayer(
       "https://api.mapbox.com/styles/v1/{id}/tiles/{z}/{x}/{y}?access_token={accessToken}",
       {
         attribution:
           'Map data (c) <a href="https://www.openstreetmap.org/">OpenStreetMap</a> contributors, <a href="https://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>, Imagery (c) <a href="https://www.mapbox.com/">Mapbox</a>',
         maxZoom: 18,
         id: "mapbox/streets-v11",
         accessToken:"pk.eyJ1IjoiYWxleGRlYnVnIiwiYSI6ImNsZ2Q4Yzl4ZTA0NDIzbG50MHVsejZkZ2MifQ.rwQUZ3NSxE3EetYpE-2KXg",
       }
     ).addTo(mapDiv);
     this.setupGeosphere(mapDiv);
     this.setupHidrosphere(mapDiv);
     this.setupAtmosphere(mapDiv);
     this.setupBiosphere(mapDiv);
     
   },

  setupGeosphere(mapDiv) {
    var icon = L.icon({
    iconUrl: geoIcon,

    iconSize:     [40, 40], // size of the icon
    iconAnchor:   [22, 94], // point of the icon which will correspond to marker's location
    popupAnchor:  [-3, -76] // point from which the popup should open relative to the iconAnchor
    });
    features.Geosphere.map((feature) => {
      L.marker([feature.location.lat, feature.location.lng], {icon: icon})
      .addTo(mapDiv)
      .bindPopup(feature.name)
      .openPopup()
      .on("click", () => {
        this.$emit("FeatureClicked", {"type": feature.type, "name": feature.name});
      })
    })
  },
  setupHidrosphere(mapDiv) {
    var icon = L.icon({
    iconUrl: hidroIcon,

    iconSize:     [40, 40], // size of the icon
    iconAnchor:   [22, 94], // point of the icon which will correspond to marker's location
    popupAnchor:  [-3, -76] // point from which the popup should open relative to the iconAnchor
    });
    features.Hidrosphere.map((feature) => {
      L.marker([feature.location.lat, feature.location.lng], {icon: icon})
      .addTo(mapDiv)
      .bindPopup(feature.name)
      .openPopup()
      .on("click", () => {
        this.$emit("FeatureClicked", {"type": feature.type, "name": feature.name});
      })
    })
  },
  setupAtmosphere(mapDiv) {
    var icon = L.icon({
    iconUrl: atmoIcon,

    iconSize:     [40, 40], // size of the icon
    iconAnchor:   [22, 94], // point of the icon which will correspond to marker's location
    popupAnchor:  [-3, -76] // point from which the popup should open relative to the iconAnchor
    });
    features.Atmosphere.map((feature) => {
      L.marker([feature.location.lat, feature.location.lng], {icon: icon})
      .addTo(mapDiv)
      .bindPopup(feature.name)
      .openPopup()
      .on("click", () => {
        this.$emit("FeatureClicked", {"type": feature.type, "name": feature.name});
      })
    })
  },
  setupBiosphere(mapDiv) {
    var icon = L.icon({
    iconUrl: bioIcon,

    iconSize:     [40, 40], // size of the icon
    iconAnchor:   [22, 94], // point of the icon which will correspond to marker's location
    popupAnchor:  [-3, -76] // point from which the popup should open relative to the iconAnchor
    });
    features.Biosphere.map((feature) => {
      L.marker([feature.location.lat, feature.location.lng], {icon: icon})
      .addTo(mapDiv)
      .bindPopup(feature.name)
      .openPopup()
      .on("click", () => {
        this.$emit("FeatureClicked", {"type": feature.type, "name": feature.name});
      })
    })
  }



  },
  mounted() {
    this.setuptMap();

  },
};
</script>

<style scoped>
#mapContainer {
  z-index: 999;
  width: 75vw;
  height: 600px;
}
/*
#container {
  display: flex;
  flex-direction: row;
  justify-content: center;
} */

</style>