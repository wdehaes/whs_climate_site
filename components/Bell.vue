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
      density2: {},
      svg: {}
    }
  },
  watch: {
    densityFieldTwo: function(newValue) {
      this.updateChart(newValue);
    }
  },
  mounted: function() {
    this.renderChart();
  },
  methods: {
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
    updateChart(val) {
      var x = d3
        .scaleLinear()
        .domain([0, 10])
        .range([0, 520]);
      var y = d3
        .scaleLinear()
        .range([240, 0])
        .domain([0, 0.4]);

      var kde = this.kernelDensityEstimator(this.kernelEpanechnikov(1), x.ticks(40));
      var density2 = kde(
        this.getValueArray(val)
      );
      this.density2 = density2;
      this.svg
        .selectAll(".density2")
        .datum(this.density2)
        .transition()
        .duration(1000)
        .attr(
          "d",
          d3
            .area()
            .curve(d3.curveBasis)
            .x(function(d) {
              return x(d[0]);
            })
            .y0(240)
            .y1(function(d) {
              return y(d[1]);
            })
        )
    },
    renderChart() {
      // set the dimensions and margins of the graph
      var margin = { top: 30, right: 30, bottom: 30, left: 50 },
        width = 600 - margin.left - margin.right,
        height = 300 - margin.top - margin.bottom;

      // append the svg object to the body of the page
      this.svg = d3
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
          this.svg
            .append("g")
            .attr("transform", "translate(0," + height + ")")
            .call(d3.axisBottom(x));

          // add the y Axis
          var y = d3
            .scaleLinear()
            .range([height, 0])
            .domain([0, 0.4]);
          this.svg.append("g").call(d3.axisLeft(y));

          // Compute kernel density estimation
          var kde = this.kernelDensityEstimator(this.kernelEpanechnikov(1), x.ticks(40));
          var density1 = kde(
            this.getValueArray(this.densityFieldOne)
          );
          var density2 = kde(
            this.getValueArray(this.densityFieldTwo)
          );

          this.density1 = density1;
          this.density2 = density2;
          // Plot the area
          this.svg
            .append("path")
            .attr("class", "density1")
            .datum(density1)
            .attr("fill", "#69b3a2")
            .attr("opacity", ".6")
            .attr("stroke", "#000")
            .attr("stroke-width", 1)
            .attr("stroke-linejoin", "round")
            .attr(
              "d",
              d3
                .area()
                .curve(d3.curveBasis)
                .x(function(d) {
                  return x(d[0]);
                })
                .y0(height)
                .y1(function(d) {
                  return y(d[1]);
                })
            );

          // Plot the area
          this.svg
            .append("path")
            .attr("class", "density2")
            .datum(this.density2)
            .attr("fill", "#404080")
            .attr("opacity", ".6")
            .attr("stroke", "#000")
            .attr("stroke-width", 1)
            .attr("stroke-linejoin", "round")
            .attr(
              "d",
              d3
                .area()
                .curve(d3.curveBasis)
                .x(function(d) {
                  return x(d[0]);
                })
                .y0(height)
                .y1(function(d) {
                  return y(d[1]);
                })
            );

      // svg.append('g')
      //   .selectAll("dot")
      //   .data(this.whsData)
      //   .enter()
      //   .append("circle")
      //     .attr("cx", (d) => { return x(d[this.densityFieldOne]); } )
      //     .attr("cy", function (d) { return 1; } )
      //     .attr("r", 1.5)
      //     .style("fill", "#69b3a2")

      // Handmade legend
      this.svg
        .append("circle")
        .attr("cx", 460)
        .attr("cy", 10)
        .attr("r", 6)
        .style("fill", "#69b3a2");
      this.svg
        .append("circle")
        .attr("cx", 460)
        .attr("cy", 30)
        .attr("r", 6)
        .style("fill", "#404080");
      this.svg
        .append("text")
        .attr("x", 480)
        .attr("y", 10)
        .text("2020")
        .style("font-size", "15px")
        .attr("alignment-baseline", "middle");
      this.svg
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
