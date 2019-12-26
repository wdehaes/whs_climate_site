<template>
  <div
    id="map"
    ref="map"
  ></div>
</template>

<script>
import carto from "@carto/carto-vl";
import mapboxgl from "@carto/mapbox-gl";
import "@carto/mapbox-gl/dist/mapbox-gl.css";
const basemaps = {
  voyager: "https://basemaps.cartocdn.com/gl/voyager-gl-style/style.json",
  positron: "https://basemaps.cartocdn.com/gl/positron-gl-style/style.json",
  "dark-matter":
    "https://basemaps.cartocdn.com/gl/dark-matter-gl-style/style.json"
};
const datasets = {
  whs: "whs_risk",
  filter: "filtered_whs"
};
export default {
  name: "Map",
  data() {
    return {
      display_map: {},
      active_layer: {}
    }
  },
  props: {
    basemap: {
      default: "positron",
      type: String
    },
    dataset: {
      default: "whs",
      type: String
    }
  },
  mounted: function() {
    this.display_map = this.createMap();
    // this.active_layer = this.createLayer("blue");
    // this.active_layer.addTo(this.display_map);
    this.switchLayer();
  },
  watch: {
    dataset: function(oldVal, newVal) {
      // this.active_layer = this.createLayer("blue");
      // this.active_layer.addTo(this.display_map);
      this.switchLayer();
    }
  },
  methods: {
    switchLayer: function() {
      const new_layer = this.createLayer("blue");
      if(Object.keys(this.active_layer).length) {
        this.active_layer.remove();
      }
      this.active_layer = new_layer;
      this.active_layer.addTo(this.display_map);
    },
    createMap: function() {
      return new mapboxgl.Map({
        container: "map",
        style: basemaps[this.basemap],
        center: [10, 38],
        zoom: 4,
        minZoom: 4,
        scrollZoom: false
      });
    },
    createLayer: function(color) {
      const source = new carto.source.Dataset(datasets[this.dataset], {
        user: "wdehaes",
        apiKey: "56cde5e603439c447a4d723e6ae3346c36796237"
      });
      const viz = new carto.Viz(
        `
      width: 4
      strokeWidth: 0.5
      strokeColor: blue
      color: blue
      `
      );
      return new carto.Layer("layer", source, viz);
    }
  }
};
</script>

<style scoped>
#map {
  height: 100%;
  width: 100%;
}
</style>
