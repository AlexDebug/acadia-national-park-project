<template>
  <div class="space-y-5 text-left px-[15%] pb-[5%]">
    
    <section>
        <p>
        Acadia National Park, located in the state of Maine, is a breathtaking natural wonder that covers over 47,000 acres of 
        land and water. One of the most important aspects of the park is its hydrosphere, which includes streams, lakes, 
        wetlands, oceans, and groundwater. In this essay, we will explore each of these components and their unique 
        characteristics and importance to the park.
        </p>
        <h6>Streams:</h6>


        <p>
        Streams are one of the most common features of Acadia National Park, and they are crucial to the park's ecosystem. 
        They provide habitats for many species of fish and wildlife, and they play an important role in regulating the water 
        cycle. One of the most notable streams in the park is Jordan Stream, which flows from Jordan Pond into the Atlantic 
        Ocean. The stream is home to brook trout and provides a vital source of water for many plants and animals in the 
        surrounding area.
        </p>
        <h6>Floods:</h6>


        <p>
        Floods are a natural occurrence in Acadia National Park, and they play an essential role in shaping the landscape. 
        They can cause erosion and sedimentation, which can create new habitats for plants and animals. However, floods can 
        also be destructive, and the park has seen several significant floods over the years. One of the most notable floods 
        occurred in 1998 when Hurricane Bonnie hit the coast of Maine, causing significant damage to many areas of the park.
        </p>
        <h6>Groundwater: </h6>


        <p>
        Groundwater is an important part of Acadia National Park's hydrosphere. It is the water that is stored underground in 
        soil and rock, and it can provide a vital source of water for plants and animals. Groundwater can also play a crucial 
        role in the formation of wetlands, which we will discuss in more detail later. One of the most important groundwater 
        sources in the park is the Eagle Lake Watershed, which provides drinking water for nearby towns and is home to many 
        species of fish and wildlife. 
        </p>
        <h6>Wetlands:</h6>


        <p>
        Wetlands are an essential part of Acadia National Park's hydrosphere. They provide habitats for many species of 
        plants and animals, including several endangered species. They also help to filter pollutants and regulate water 
        flow, which can help to prevent flooding and erosion. One of the most notable wetlands in the park is the Great Meadow, 
        which is home to several rare and endangered plant species. <b>Over 20 percent of Acadia is classified as wetland</b>
        </p>
        <h6>Oceans:</h6>


        <p>
        Acadia National Park is located on the coast of Maine, and the ocean plays an essential role in its hydrosphere. 
        The ocean provides a habitat for many species of fish and marine mammals, and it is also an important source of food 
        for the surrounding communities. One of the most notable ocean features in the park is the Schoodic Peninsula, which 
        offers stunning views of the coastline and is home to several species of seabirds.
        </p>
        <h6>Lakes and Ponds:</h6>


        <p>
        Acadia National Park is home to many lakes and ponds, which provide habitats for many species of fish and wildlife. 
        They also offer opportunities for recreation, such as swimming, boating, and fishing. One of the most notable lakes 
        in the park is Eagle Lake, which is surrounded by forests and offers stunning views of the surrounding mountains. The 
        lake is also home to several species of fish, including brook trout and landlocked salmon.
        </p>
        <p>
        In conclusion, the hydrosphere of Acadia National Park is a vital part of its ecosystem. Streams, floods, groundwater, 
        wetlands, oceans, lakes, and ponds all play important roles in regulating the water cycle and providing habitats for 
        many species of plants and animals. By preserving and protecting these resources, we can ensure that Acadia National 
        Park remains a natural wonder for generations to come.
        </p>
      <div id="ph">
        <h1 class="text-center">pH in water</h1>
      </div>
      <div id="alk">
        <h1 class="text-center">Alkalinity in water</h1>
      </div>
    </section>
  </div>
</template>

<script>
import * as d3 from 'd3'
import ph_and_alkalinity from './../../../assets/data/ph_and_alkalinity.json'
// import temp_oxg_average from './../../../assets/data/temp_oxg_average.json'

ph_and_alkalinity.forEach((d) => {
  d.Date = new Date(d.Date)
})

export default {
    mounted() {
      this.drawCharts()
    },
    beforeUnmount() {
      document.querySelector("#ph > svg").remove()
      document.querySelector("#alk > svg").remove()
    },
    methods: {
      drawCharts() {
        this.drawPH()
        this.drawAlk()
      },
      drawPH() {
        let data = ph_and_alkalinity

        const margin = { top: 20, right: 20, bottom: 30, left: 50 };
        const width = 960 - margin.left - margin.right;
        const height = 500 - margin.top - margin.bottom;

        let svg = d3.select("#ph")
        .append("svg")
        .attr(
            "viewBox",
            [0, 0, width + margin.left + margin.right, 
            height + margin.top + margin.bottom]
        )
        .style("background-color", "#F2E2CD")
        .append("g")
        .attr("transform", "translate(" + margin.left + "," + margin.top + ")");

        const x = d3.scaleTime().domain(d3.extent(data, (d) => d.Date)).range([0, width]);
        const y = d3.scaleLinear().domain(d3.extent(data, (d) => d.pH)).range([height, 0]);

        const xAxis = d3.axisBottom(x);
        const yAxis = d3.axisLeft(y);

        svg.append("g")
          .attr("stroke", '#555358')
          .attr("transform", "translate(0," + height + ")")
          .call(xAxis);

        svg.append("g")
          .attr("stroke", '#555358')
          .call(yAxis);

        const line = d3.line()
          .x((d) => x(d.Date))
          .y((d) => y(d.pH));

        svg.append("path")
          .datum(data)
          .attr("fill", "none")
          .attr("stroke", "#FF6666")
          .attr("stroke-width", 1.5)
          .attr("id", "phLine")
          .attr("d", line);
      },
      drawAlk() {
        let data = ph_and_alkalinity

        const margin = { top: 20, right: 20, bottom: 30, left: 50 };
        const width = 960 - margin.left - margin.right;
        const height = 500 - margin.top - margin.bottom;

        let svg = d3.select("#alk")
          .append("svg")
          .attr(
            "viewBox",
            [0, 0, width + margin.left + margin.right, 
            height + margin.top + margin.bottom]
          )
          .style("background-color", "#F2E2CD")
          .append("g")
          .attr("transform", "translate(" + margin.left + "," + margin.top + ")");

        const x = d3.scaleTime().domain(d3.extent(data, (d) => d.Date)).range([0, width]);
        const y = d3.scaleLinear().domain(d3.extent(data, (d) => d.Alkalinity)).range([height, 0]);

        const xAxis = d3.axisBottom(x);
        const yAxis = d3.axisLeft(y);

        svg.append("g")
          .attr("transform", "translate(0," + height + ")")
          .call(xAxis);

        svg.append("g")
          .call(yAxis);

        const line = d3.line()
                      .x((d) => x(d.Date))
                      .y((d) => y(d.Alkalinity));

        svg.append("g")
          .append("path")
          .datum(data)
          .attr("fill", "none")
          .attr("stroke", "#FF6666")
          .attr("stroke-width", 1.5)
          .attr("id", "phLine")
          .attr("d", line);

      }
    }
  }
</script>

<style>
</style>