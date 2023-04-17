<template>
  <div class="space-y-5 text-left px-[15%] pb-[5%]">
    <p>
    Acadia National Park is a stunning natural landscape located on Mount Desert Island in Maine. The park is renowned for its 
    scenic beauty, breathtaking vistas, and rugged coastline. The park is an excellent example of the unique atmospheric 
    structure, components, weather systems, and climate patterns that exist in the region. We will explore these elements in 
    detail and demonstrate how they contribute to the unique atmosphere of Acadia National Park.
    </p>
    <h6>Atmospheric Structure:</h6>


    <p>
    Acadia National Park's location along the Maine coastline makes it a unique and fascinating region to study atmospheric 
    structure. The park's position at the intersection of the Gulf of Maine and the Atlantic Ocean creates a complex atmospheric
     structure. The park's coastline is subject to marine air masses that have a significant influence on the park's climate and 
     weather patterns. The cold Labrador Current flows southward from the Arctic, bringing cold air masses to the region. As 
     these air masses move across the relatively warmer waters of the Gulf of Maine, they become moist and unstable, leading to 
     frequent fog and cloud cover.
    </p>
    <p>
    The park's mountainous terrain also contributes to the atmospheric structure of the region. The high elevations of the 
    mountains create an orographic effect, which alters the atmospheric circulation patterns in the region. As the moist marine 
    air masses move up the mountain slopes, they cool and condense, leading to increased precipitation in the form of snow and 
    rain.
    </p>
    <h6>Atmospheric Components:</h6>


    <p>
    The atmosphere of Acadia National Park is composed of various components, including gases, particles, and water vapor. 
    The air is made up of nitrogen, oxygen, argon, and carbon dioxide, with trace amounts of other gases such as neon, helium, 
    methane, and hydrogen. The particles in the atmosphere include dust, pollen, and smoke particles, which can impact air 
    quality and visibility in the park.
    </p>
    <p>
    Water vapor is a crucial component of the atmosphere in Acadia National Park, and its presence influences the weather 
    patterns in the region. The park's location near the coast and the high elevation of the mountains create an ideal 
    environment for the formation of clouds and fog. The moisture-laden air masses that move across the Gulf of Maine and 
    collide with the mountains create a perfect recipe for cloud and fog formation, which can often obscure the park's stunning 
    vistas.
    </p>
    <h6>Weather Systems and Severe Weather:</h6>


    <p>
    Acadia National Park experiences a diverse range of weather systems, ranging from mild to severe. The park's location along 
    the coast means that it is subject to the influence of both maritime and continental air masses. Maritime air masses tend 
    to be humid and warm, while continental air masses tend to be drier and cooler. As these air masses collide in the region, 
    they can create severe weather conditions such as thunderstorms, tornadoes, and hurricanes.
    </p>
    <p>
    The park's location also makes it vulnerable to coastal storms, which can produce high winds, heavy rainfall, and coastal 
    flooding. The park's rugged coastline is subject to erosion and damage from the strong wave action associated with these 
    storms.
    </p>
    <h6>Climate Patterns:</h6>


    <p>
    Acadia National Park has a unique climate due to its location at the intersection of the Gulf of Maine and the Atlantic 
    Ocean. The park's climate is classified as humid continental, with cold winters and mild summers. The park's coastal 
    location moderates the temperature, resulting in cooler summers and warmer winters than areas further inland.
    </p>
    <p>
    The park's location also makes it vulnerable to climate change, with rising sea levels and changes in temperature and 
    precipitation patterns potentially impacting the park's ecosystems and wildlife. The park's delicate balance of flora and 
    fauna could be at risk if the climate patterns in the region were to change significantly.
    </p>
    <p>
    In conclusion, Acadia National Park is a unique and beautiful natural landscape that is shaped by its atmospheric structure, 
    components, weather systems, and climate patterns. The park's location along the Maine coast creates a complex atmospheric 
    environment that is influenced by both marine and continental
    </p>
    <div id="tavg">
      <h1 class="text-center">Temperature Average</h1>
    </div>
    <div id="prcp">
      <h1 class="text-center">Precipitations</h1>
    </div>
  </div>
</template>

<script>
import * as d3 from 'd3'
import tavg from './../../../assets/data/tavg.json'
import prcp from './../../../assets/data/prcp.json'

tavg.forEach((d) => {
  d.DATE = new Date(d.DATE)
})

prcp.forEach((d) => {
  d.DATE = new Date(d.DATE)
})

export default {
  mounted() {
    this.drawCharts()
  },
  beforeUnmount() {
      document.querySelector("#tavg > svg").remove()
      document.querySelector("#prcp > svg").remove()
    },
  methods: {
    drawCharts() {
      this.draw_prcp();
      this.draw_tavg();
    },
    draw_tavg() {
      let data = tavg

      const margin = { top: 20, right: 20, bottom: 30, left: 50 };
      const width = 960 - margin.left - margin.right;
      const height = 500 - margin.top - margin.bottom;

      let svg = d3.select("#tavg")
      .append("svg")
      .attr(
          "viewBox",
          [0, 0, width + margin.left + margin.right, 
          height + margin.top + margin.bottom]
      )
      .style("background-color", "#F2E2CD")
      .append("g")
      .attr("transform", "translate(" + margin.left + "," + margin.top + ")");

      const x = d3.scaleTime().domain(d3.extent(data, (d) => d.DATE)).range([0, width]);
      const y = d3.scaleLinear().domain(d3.extent(data, (d) => d.TAVG)).range([height, 0]);

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
        .x((d) => x(d.DATE))
        .y((d) => y(d.TAVG));

      svg.append("path")
        .datum(data)
        .attr("fill", "none")
        .attr("stroke", "#FF6666")
        .attr("stroke-width", 1.5)
        .attr("id", "phLine")
        .attr("d", line);
    },
    draw_prcp() {
      let data = prcp

      const margin = { top: 20, right: 20, bottom: 30, left: 50 };
      const width = 960 - margin.left - margin.right;
      const height = 500 - margin.top - margin.bottom;

      let svg = d3.select("#prcp")
      .append("svg")
      .attr(
          "viewBox",
          [0, 0, width + margin.left + margin.right, 
          height + margin.top + margin.bottom]
      )
      .style("background-color", "#F2E2CD")
      .append("g")
      .attr("transform", "translate(" + margin.left + "," + margin.top + ")");

      const x = d3.scaleTime().domain(d3.extent(data, (d) => d.DATE)).range([0, width]);
      const y = d3.scaleLinear().domain(d3.extent(data, (d) => d.PRCP)).range([height, 0]);

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
        .x((d) => x(d.DATE))
        .y((d) => y(d.PRCP));

      svg.append("path")
        .datum(data)
        .attr("fill", "none")
        .attr("stroke", "#FF6666")
        .attr("stroke-width", 1.5)
        .attr("id", "phLine")
        .attr("d", line);
    },

  }
}
</script>

<style>

</style>