<template>
  <div>
    <svg class="bell"></svg>
  </div>
</template>

<script>
import * as d3 from "d3";
export default {
  props: {
    whsData: Array
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
    renderChart() {
      // set the dimensions and margins of the graph
      var margin = { top: 30, right: 30, bottom: 30, left: 50 },
        width = 600 - margin.left - margin.right,
        height = 500 - margin.top - margin.bottom;

      // append the svg object to the body of the page
      var svg = d3
        .select("svg.bell")
        .attr("width", width + margin.left + margin.right)
        .attr("height", height + margin.top + margin.bottom)
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
            .domain([0, 0.20]);
          svg.append("g").call(d3.axisLeft(y));

          // Compute kernel density estimation
          var kde = this.kernelDensityEstimator(this.kernelEpanechnikov(3), x.ticks(40));
          var density1 = kde(
            this.getValueArray('column_2020_rcp4_5_flood')
          );
          var density2 = kde(
            this.getValueArray('column_2100_high_end_flood')
          );

          // Plot the area
          svg
            .append("path")
            .attr("class", "mypath")
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
          svg
            .append("path")
            .attr("class", "mypath")
            .datum(density2)
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


      // Handmade legend
      svg
        .append("circle")
        .attr("cx", 300)
        .attr("cy", 30)
        .attr("r", 6)
        .style("fill", "#69b3a2");
      svg
        .append("circle")
        .attr("cx", 300)
        .attr("cy", 60)
        .attr("r", 6)
        .style("fill", "#404080");
      svg
        .append("text")
        .attr("x", 320)
        .attr("y", 30)
        .text("2020")
        .style("font-size", "15px")
        .attr("alignment-baseline", "middle");
      svg
        .append("text")
        .attr("x", 320)
        .attr("y", 60)
        .text("2100")
        .style("font-size", "15px")
        .attr("alignment-baseline", "middle");
    }

  }
};
</script>

<style>
</style>
