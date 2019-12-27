<template>
  <div class="svg-container">
    <svg class="bell" v-bind:id="svgId"></svg>
  </div>
</template>

<script>
import * as d3 from "d3";
export default {
  props: {
    whsData: Array,
    densityFieldOne: String,
    densityFieldTwo: String,
    svgId: String
  },
  data() {
    return {
      density1: {},
      density2: {}
    }
  },
  mounted: function() {
    this.renderChart();
  },
  methods: {
    findDensityValue(value) {

    },
    getValueArray(field) {
      return this.whsData.map(
      (element) => element[field]
      )
    },
    // Function to compute density
    kernelDensityEstimator(kernel, X) {
      return function(V) {
        return X.map(function(x) {
          return [
            x,
            d3.mean(V, function(v) {
              return kernel(x - v);
            })
          ];
        });
      };
    },
    kernelEpanechnikov(k) {
      return function(v) {
        return Math.abs((v /= k)) <= 1 ? (0.75 * (1 - v * v)) / k : 0;
      };
    },
    renderChart() {
      // set the dimensions and margins of the graph
      var margin = { top: 30, right: 30, bottom: 30, left: 50 },
        width = 600 - margin.left - margin.right,
        height = 300 - margin.top - margin.bottom;

      // append the svg object to the body of the page
      var svg = d3
        .select("#" + this.svgId)
        .attr("preserveAspectRatio", "xMinYMin meet")
        .attr("viewBox", "0 0 600 300")
        .classed("svg-content", true)
        // .attr("width", width + margin.left + margin.right)
        // .attr("height", height + margin.top + margin.bottom)
        .append("g")
        .attr("transform", "translate(" + margin.left + "," + margin.top + ")");

      // get the data

          // add the x Axis
          var x = d3
            .scaleLinear()
            .domain([0, 10])
            .range([0, width]);
          svg
            .append("g")
            .attr("transform", "translate(0," + height + ")")
            .call(d3.axisBottom(x));

          // add the y Axis
          var y = d3
            .scaleLinear()
            .range([height, 0])
            .domain([0, 20]);
          svg.append("g").call(d3.axisLeft(y));

          // Compute kernel density estimation
          var histogram1 = d3.histogram()
              .value(function(d) { return d.column_2020_rcp4_5_flood; })   // I need to give the vector of value
              .domain(x.domain())  // then the domain of the graphic
              .thresholds(x.ticks(70)); // then the numbers of bins


          var histogram2 = d3.histogram()
              .value(function(d) { return d.column_2100_high_end_flood; })   // I need to give the vector of value
              .domain(x.domain())  // then the domain of the graphic
              .thresholds(x.ticks(70)); // then the numbers of bins
          // Plot the area

          var bins1 = histogram1(this.whsData);
          var bins2 = histogram2(this.whsData);

    svg.selectAll("rect")
          .data(bins1)
          .enter()
          .append("rect")
            .attr("x", 1)
            .attr("transform", function(d) { return "translate(" + x(d.x0) + "," + y(d.length) + ")"; })
            .attr("width", function(d) { return x(d.x1) - x(d.x0) -1 ; })
            .attr("height", function(d) { return height - y(d.length); })
            .style("fill", "#69b3a2")
            .style("opacity", 0.6)

    svg.selectAll("rect2")
        .data(bins2)
        .enter()
        .append("rect")
          .attr("x", 1)
          .attr("transform", function(d) { return "translate(" + x(d.x0) + "," + y(d.length) + ")"; })
          .attr("width", function(d) { return x(d.x1) - x(d.x0) -1 ; })
          .attr("height", function(d) { return height - y(d.length); })
          .style("fill", "#404080")
          .style("opacity", 0.6)

      // Handmade legend
      svg
        .append("circle")
        .attr("cx", 460)
        .attr("cy", 10)
        .attr("r", 6)
        .style("fill", "#69b3a2");
      svg
        .append("circle")
        .attr("cx", 460)
        .attr("cy", 30)
        .attr("r", 6)
        .style("fill", "#404080");
      svg
        .append("text")
        .attr("x", 480)
        .attr("y", 10)
        .text("2020")
        .style("font-size", "15px")
        .attr("alignment-baseline", "middle");
      svg
        .append("text")
        .attr("x", 480)
        .attr("y", 30)
        .text("2100")
        .style("font-size", "15px")
        .attr("alignment-baseline", "middle");
    }

  }
};
</script>

<style>
.svg-container {
    display: inline-block;
    position: relative;
    width: 100%;
    padding-bottom: 55%;
    vertical-align: top;
    overflow: hidden;
}
.svg-content {
    display: inline-block;
    position: absolute;
    top: 0;
    left: 0;
}
</style>
