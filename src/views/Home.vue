<template>
  <div class="home">
    <p>first commit</p>
    <button @click="backPath">back record</button>
    <div style="height: 500px">
      <MglMap
        :accessToken="accessToken"
        :mapStyle.sync="mapStyle"
        :center="[-122.4835, 37.83]"
        :zoom="14"
        :attributionControl="false"
      >
        <MglGeojsonLayer
          :sourceId="pathData.id"
          :source="pathData.sourceData"
          :layerId="layer.id"
          :layer="layer"
        />
        <MglMarker :coordinates="coordinates">
          <font-awesome-icon :icon="['fas', 'truck']" size="2x" slot="marker" />
          <MglPopup>
            <div>Hello, I'm popup!</div>
          </MglPopup>
        </MglMarker>
      </MglMap>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
// import Mapbox from "mapbox-gl";
import { MglMap, MglGeojsonLayer, MglMarker, MglPopup } from "vue-mapbox";

export default {
  name: "Home",
  components: {
    MglMap,
    MglGeojsonLayer,
    MglMarker,
    MglPopup,
  },
  data() {
    return {
      // your access token. Needed if you using Mapbox maps
      accessToken: process.env.VUE_APP_MAPTOKEN,
      // your map style
      mapStyle: "mapbox://styles/jamie0510/ckxijwvzj0mad15n4ckyxh580",
      // defaultInput: "Bodhgaya",
      pathData: {
        id: "01",
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
      },
      layer: {
        id: "route01",
        type: "line",
        source: "01",
        layout: {
          "line-join": "round",
          "line-cap": "round",
        },
        paint: {
          "line-color": "red",
          "line-width": 8,
        },
      },
      coordinates: [-122.483696, 37.833818],
    };
  },
  created() {
    // We need to set mapbox-gl library here in order to use it in template
    // this.mapbox = Mapbox;
  },
  methods: {
    backPath() {
      this.pathData.sourceData.data.geometry.coordinates.splice(0, 1);
      this.coordinates = this.pathData.sourceData.data.geometry.coordinates[0];
    },
    onMapLoaded(event) {
      console.log(event);
    },
  },
};
</script>
