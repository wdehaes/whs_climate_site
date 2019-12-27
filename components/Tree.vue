<template>
  <div>
    <h4 class="title is-6 has-text-centered">Global warming: chain of events in a nutshell</h4>
    <svg class="tree"></svg>
  </div>
</template>

<script>
import * as d3 from "d3";
export default {
  mounted: function() {
    this.renderChart();
  },
  methods: {
    renderChart() {
      var treeData = {
        name: "Earth's temperature increases",
        children: [
          {
            name: "Water in the oceans and seas expands",
            children: [
              {
                name: "Sea levels rise",
                children: [
                  {
                    name: "Waves become higher",
                    children: [
                      {
                        name: "Floods are more frequent and intense"
                      },
                      {
                        name: "Beaches and cliffs erode faster"
                      }
                    ]
                  }
                ]
              }
            ]
          }
        ]
      };

      // set the dimensions and margins of the diagram
      var margin = { top: 40, right: 90, bottom: 50, left: 90 },
        width = 600 - margin.left - margin.right,
        height = 500 - margin.top - margin.bottom;

      // declares a tree layout and assigns the size
      var treemap = d3.tree().size([width, height]);

      //  assigns the data to a hierarchy using parent-child relationships
      var nodes = d3.hierarchy(treeData);

      // maps the node data to the tree layout
      nodes = treemap(nodes);

      // append the svg obgect to the body of the page
      // appends a 'group' element to 'svg'
      // moves the 'group' element to the top left margin
      var svg = d3
          .select("svg.tree")
          // .attr("width", width + margin.left + margin.right)
          // .attr("height", height + margin.top + margin.bottom),
        .attr("preserveAspectRatio", "xMinYMin meet")
        .attr("viewBox", "0 0 600 500")
        var g = svg
          .append("g")
          .attr(
            "transform",
            "translate(" + margin.left + "," + margin.top + ")"
          );

      // adds the links between the nodes
      var link = g
        .selectAll(".link")
        .data(nodes.descendants().slice(1))
        .enter()
        .append("path")
        .attr("class", "link")
        .attr("d", function(d) {
          return (
            "M" +
            d.x +
            "," +
            d.y +
            "C" +
            d.x +
            "," +
            (d.y + d.parent.y) / 2 +
            " " +
            d.parent.x +
            "," +
            (d.y + d.parent.y) / 2 +
            " " +
            d.parent.x +
            "," +
            d.parent.y
          );
        });

      // adds each node as a group
      var node = g
        .selectAll(".node")
        .data(nodes.descendants())
        .enter()
        .append("g")
        .attr("class", function(d) {
          return "node" + (d.children ? " node--internal" : " node--leaf");
        })
        .attr("transform", function(d) {
          return "translate(" + d.x + "," + d.y + ")";
        });

      // adds the circle to the node
      // node.append("circle").attr("r", 10);
      node.append('path')
      .attr('d', function(d) {
        // https://groups.google.com/forum/#!topic/d3-js/kHONjIWjAA0
        return 'M ' + 0 +' '+ 5 + ' l 8 -17 l -16 0 z';
      });

      // adds the text to the node
      node
        .append("text")
        .attr("dy", ".35em")
        .attr("y", function(d) {
          // return d.children ? -20 : 20;
          return 20;
        })
        .style("text-anchor", "middle")
        .text(function(d) {
          return d.data.name;
        });
    }
  }
};
</script>
<style>
.node circle {
  fill: #fff;
  stroke: steelblue;
  stroke-width: 1px;
}

.node text {
  font-size: .8em;
  font-weight: 400;
  line-height: 1.5;
  font-family: BlinkMacSystemFont, -apple-system, "Segoe UI", "Roboto", "Oxygen", "Ubuntu", "Cantarell", "Fira Sans", "Droid Sans", "Helvetica Neue", "Helvetica", "Arial", sans-serif;
}

.node--internal text {
  text-shadow: 0 1px 0 #fff, 0 -1px 0 #fff, 1px 0 0 #fff, -1px 0 0 #fff;
}

.link {
  fill: none;
  stroke: #ccc;
  stroke-width: 1px;
}
</style>
