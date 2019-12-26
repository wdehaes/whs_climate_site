<template>
  <div>
    <svg class="graph"></svg>
  </div>
</template>

<script>
import * as d3 from "d3";
export default {
  props: {
    input: Array
  },
  mounted() {
    this.renderChart();
  },
  methods: {
    renderChart() {
      var margin = { top: 10, right: 30, bottom: 30, left: 60 },
        width = 460 - margin.left - margin.right,
        height = 400 - margin.top - margin.bottom;
      // append the svg object to the body of the page
      var svg = d3
        .select("svg.graph")
        .attr("width", width + margin.left + margin.right)
        .attr("height", height + margin.top + margin.bottom)
        .append("g")
        .attr("transform", "translate(" + margin.left + "," + margin.top + ")");
      var x = d3
        .scaleLinear()
        .domain([1999, 2019]
        )
        .range([0, width]);
      svg
        .append("g")
        .attr("transform", "translate(0," + height + ")")
        .call(d3.axisBottom(x).tickFormat(d3.format("d")));
      // Add Y axis
      var y = d3
        .scaleLinear()
        .domain([0, 70])
        .range([height, 0]);
      svg.append("g").call(d3.axisLeft(y));
      // Add the line
      svg
        .append("path")
        .datum(this.input)
        .attr("fill", "none")
        .attr("stroke", "#69b3a2")
        .attr("stroke-width", 1.5)
        .attr(
          "d",
          d3
            .line()
            .x(function(d) {
              return x(d.year);
            })
            .y(function(d) {
              return y(d.value);
            })
        );
      // Add the points
      svg
        .append("g")
        .selectAll("dot")
        .data(this.input)
        .enter()
        .append("circle")
        .attr("cx", function(d) {
          return x(d.year);
        })
        .attr("cy", function(d) {
          return y(d.value);
        })
        .attr("r", 5)
        .attr("fill", "#69b3a2");
    }
  }
};
</script>

<style>
</style>
