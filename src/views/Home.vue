<template>
  <div class="home">
    <p>first commit</p>
    <div style="height: 500px">
      <MglMap
        :accessToken="accessToken"
        :mapStyle.sync="mapStyle"
        :center="[-122, 37]"
        :zoom="12"
      >
        <MglGeojsonLayer
          sourceId="route"
          :source="sourceData"
          layerId="route"
          :layer="layer"
        />
      </MglMap>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from "@/components/HelloWorld.vue";
import Mapbox from "mapbox-gl";
import { MglMap, MglGeojsonLayer } from "vue-mapbox";

export default {
  name: "Home",
  components: {
    MglMap,
    MglGeojsonLayer,
    // MglGeocoderControl
  },
  data() {
    return {
      // your access token. Needed if you using Mapbox maps
      accessToken: process.env.VUE_APP_MAPTOKEN,
      // your map style
      mapStyle: "mapbox://styles/jamie0510/ckxijwvzj0mad15n4ckyxh580",
      // defaultInput: "Bodhgaya",
      sourceData: {
        type: "geojson",
        data: {
          type: "Feature",
          properties: {},
          geometry: {
            type: "LineString",
            coordinates: [
              [-122.483696, 37.833818],
              [-122.483482, 37.833174],
              [-122.483396, 37.8327],
              [-122.483568, 37.832056],
              [-122.48404, 37.831141],
              [-122.48404, 37.830497],
              [-122.483482, 37.82992],
              [-122.483568, 37.829548],
              [-122.48507, 37.829446],
              [-122.4861, 37.828802],
              [-122.486958, 37.82931],
              [-122.487001, 37.830802],
              [-122.487516, 37.831683],
              [-122.488031, 37.832158],
              [-122.488889, 37.832971],
              [-122.489876, 37.832632],
              [-122.490434, 37.832937],
              [-122.49125, 37.832429],
              [-122.491636, 37.832564],
              [-122.492237, 37.833378],
              [-122.493782, 37.833683],
            ],
          },
        },
      },
      layer: {
        id: "route",
        type: "line",
        source: "route",
        layout: {
          "line-join": "round",
          "line-cap": "round",
        },
        paint: {
          "line-color": "red",
          "line-width": 8,
        },
      },
    };
  },
  created() {
    // We need to set mapbox-gl library here in order to use it in template
    this.mapbox = Mapbox;
  },
  methods: {
    async onMapLoaded(event) {
      // Here we cathing 'load' map event
      const asyncActions = event.component.actions;
      await asyncActions.addSource("route", {
        type: "geojson",
        data: {
          type: "Feature",
          properties: {},
          geometry: {
            type: "LineString",
            coordinates: [
              [113, 37.833818],
              [113, 37.833174],
              [113, 37.8327],
              [113, 37.832056],
              [113, 37.831141],
              [113, 37.830497],
              [113, 37.82992],
              [113, 37.829548],
              [113, 37.829446],
              [113, 37.828802],
              [113, 37.82931],
              [113, 37.830802],
            ],
          },
        },
      });
      await asyncActions.addLayer({
        id: "route",
        type: "line",
        source: "route",
        layout: {
          "line-join": "round",
          "line-cap": "round",
        },
        paint: {
          "line-color": "#888",
          "line-width": 8,
        },
      });
    },
  },
};
</script>
