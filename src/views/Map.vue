<template>
  <div class="map-container">
    <div id="map-container"></div>
    <Navigation @zoomIn="zoomIn" @zoomOut="zoomOut" @resetMap="resetMap"></Navigation>
  </div>
</template>

<script>
// @ is an alias to /src
import Navigation from "@/components/Navigation.vue";

export default {
  name: "mapView",
  components: { Navigation },
  data() {
    return {
      map: null,
      OSMUrl: "https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png"
    };
  },
  mounted() {
    this.map = this.$utils.map.createMap("map-container", {
      zoomControl: false
    });
    this.$utils.map.createTileLayer(this.map, this.OSMUrl, {});
    this.map.setView([22.352, 114.17], 11);
  },
  methods: {
    zoomIn() {
      this.map.zoomIn();
    },
    zoomOut() {
      this.map.zoomOut();
    },
    resetMap() {
      this.map.flyTo([22.352, 114.17], 11);
    }
  }
};
</script>
<style lang="less">
.map-container {
  position: absolute;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
}
#map-container {
  width: 100%;
  height: 100%;
}
</style>
