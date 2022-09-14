<template>
  <div id="graph-editor">
    <button class="btn btn-primary" id="add-node" @click="addNode">Add Node</button>
    Graph Editor
    <div id="graph-container">

    </div>
  </div>
</template>
<script>
import "jquery/dist/jquery"
import "lodash/lodash"
import "backbone/backbone-min"
import * as joint from "jointjs"

var lastRect;
var graph;

// function addNode() {
//   let rect2 = lastRect.clone();
//   rect2.translate(0, 30);
//   rect2.attr('label/text', 'World!');
//   rect2.addTo(graph);
//
//   let link = new joint.shapes.standard.Link();
//   link.source(rect);
//   link.target(rect2);
//   link.addTo(graph);
//   lastRect = rect2;
// }

export default {
  name: 'GraphEditor',

  methods: {
    addNode() {
      let rect2 = lastRect.clone();
      rect2.translate(0, 60);
      rect2.attr('label/text', 'World!');
      rect2.addTo(graph);

      let link = new joint.shapes.standard.Link();
      link.source(lastRect);
      link.target(rect2);
      link.addTo(graph);
      lastRect = rect2;
    }
  },

  mounted() {
    var namespace = joint.shapes;

    graph = new joint.dia.Graph({}, { cellNamespace: namespace });

    var paper = new joint.dia.Paper({
      el: document.getElementById('graph-container'),
      model: graph,
      width: 600,
      height: 700,
      gridSize: 1,
      cellViewNamespace: namespace
    });

    let rect = new joint.shapes.standard.Rectangle();
    rect.position(100, 30);
    rect.resize(100, 40);
    rect.attr({
      body: {
        fill: 'blue'
      },
      label: {
        text: 'Hello',
        fill: 'white'
      }
    });
    rect.addTo(graph);
    lastRect = rect;
  }
}
</script>