<template>
  <div class="home">
    <p>first commit</p>
    <div style="height: 500px">
      <MglMap :accessToken="accessToken" :mapStyle="mapStyle" />
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from "@/components/HelloWorld.vue";
import Mapbox from "mapbox-gl";
import { MglMap } from "vue-mapbox";

export default {
  name: "Home",
  components: { MglMap },
  data() {
    return {
      // your access token. Needed if you using Mapbox maps
      accessToken:
        "pk.eyJ1IjoiamFtaWUwNTEwIiwiYSI6ImNreGlqZ295MjBsN3AzMXF3YnhqYmpndmsifQ.sw_aNvmT2e2vN9TCBGayQg",
      // your map style
      mapStyle: "mapbox://styles/jamie0510/ckxijwvzj0mad15n4ckyxh580",
    };
  },
  created() {
    // We need to set mapbox-gl library here in order to use it in template
    this.mapbox = Mapbox;
  },
};
</script>
