<template>
  <div class="scenario">
      <svg v-bind:id="svgField"></svg>
    </div>
</template>

<script>
import * as d3 from "d3";
export default {
  props: {
    name: String,
    tMean: Number,
    tLow: Number,
    tHigh: Number,
    sMean: Number,
    sLow: Number,
    sHigh: Number,
    field: String
  },
  mounted() {
    this.renderChart();
  },
  computed: {
    svgField: function() {
      return 'svg_' + this.field;
    }
  },
  methods: {
    renderChart() {
      var margin = { top: 5, right: 5, bottom: 5, left: 5 },
        width = 200 - margin.left - margin.right,
        height = 40 - margin.top - margin.bottom;

      var svg = d3.select("#" + this.svgField)
        .attr("preserveAspectRatio", "xMinYMin meet")
        .attr("viewBox", "0 0 200 40")
        .append("g")
        .attr("transform", "translate(" + margin.left + "," + margin.top + ")");
      // add the x Axis
      var x = d3
        .scaleLinear()
        .domain([0, 5])
        .range([0, width]);
      svg
        .append("g")
        .attr("transform", "translate(0," + height + ")")
        .call(d3.axisBottom(x));
    }
  },
}
</script>

<style scoped>
.scenario {
  width: 100%;
}
</style>
