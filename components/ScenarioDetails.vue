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
        .attr("viewBox", "0 0 200 30")
        .append("g")
        .attr("transform", "translate(" + margin.left + "," + margin.top + ")");
      // add the x Axis
      var x = d3
        .scaleLinear()
        .domain([0, 6])
        .range([0, 72]);
      svg
        .append("g")
        .attr("transform", "translate(0," + 5 + ")")
        .call(d3.axisBottom(x).ticks(2).tickSize(3));

      svg.append('rect')
          .attr('x', this.tMean * 12 - 1)
          .attr('y', -4)
          .attr('width', 1)
          .attr('height', 12)
          .attr('fill', "red")

      svg.append('rect')
          .attr('x', this.tLow * 12)
          .attr('y', 0)
          .attr('width', 12*(this.tHigh - this.tLow))
          .attr('height', 4)
          .attr('fill', "#69b3a2")
      var xT = d3
        .scaleLinear()
        .domain([0, 1])
        .range([0, 72]);
      svg
        .append("g")
        .attr("transform", "translate(" + 110 + "," + 5 + ")")
        .call(d3.axisBottom(xT).ticks(2).tickSize(3));

      svg.append('rect')
          .attr('x', 110 + this.sMean * 72 - 1)
          .attr('y', -4)
          .attr('width', 1)
          .attr('height', 12)
          .attr('fill', "red")

      svg.append('rect')
          .attr('x', 110 + this.sLow * 72)
          .attr('y', 0)
          .attr('width', 72*(this.sHigh - this.sLow))
          .attr('height', 4)
          .attr('fill', "#404080")
    }
  },
}
</script>

<style scoped>
.scenario {
  width: 100%;
}
g text { font: 8px sans-serif; }
</style>
