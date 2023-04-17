<template>
  <div class="space-y-5 text-left px-[15%] pb-[5%]">
    <p>
    Acadia National Park is a remarkable natural reserve located on Mount Desert Island, Maine, in the northeastern part of the 
    United States. It is a haven for wildlife and plant diversity, comprising over 47,000 acres of land, and it is a popular 
    destination for visitors and nature enthusiasts from all around the world.
    </p>
    <p>
    The park is renowned for its stunning views of the Atlantic Ocean, its towering granite peaks, and its impressive array of 
    wildlife. It is home to a diverse range of plant and animal species that are unique to the region and add to the park's 
    natural beauty.
    </p>
    <p>
    The park's wildlife is a significant attraction, with visitors often sighting mammals, birds, and marine life in their 
    natural habitat. Some of the most commonly sighted animals in the park include white-tailed deer, black bears, moose, 
    coyotes, red foxes, raccoons, and beavers. Visitors can also see more elusive animals such as bobcats, lynx, and even the 
    occasional mountain lion.
    </p>
    <p>
    One of the most fascinating animals in Acadia National Park is the bald eagle, which is the symbol of the United States. 
    These majestic birds of prey can be found nesting on the cliffs and islands along the coast, and their distinctive white 
    head and tail make them easy to spot. Other notable birds in the park include the peregrine falcon, osprey, loon, and a 
    variety of songbirds.
    </p>
    <p>
    In addition to the park's mammals and birds, the marine life in the surrounding waters is equally impressive. Visitors can 
    see a range of marine creatures such as harbor seals, porpoises, whales, and dolphins. The waters of Acadia National Park 
    are also home to a variety of fish, including cod, haddock, and Atlantic salmon.
    </p>
    <p>
    Acadia National Park's plant life is just as diverse as its wildlife, with over 1,000 species of plants and wildflowers. 
    The park's forests are primarily composed of spruce, fir, and pine trees, which provide a habitat for a range of animals 
    such as red squirrels, chipmunks, and white-tailed deer. Visitors can also see a variety of wildflowers, such as lupines, 
    fireweed, and Indian pipe, which add to the park's natural beauty.
    </p>
    <p>
    One of the most unique aspects of Acadia National Park is the intertidal zone, where the ocean meets the land. This area is 
    home to a range of plant and animal species, including seaweed, barnacles, mussels, crabs, and starfish. The intertidal zone 
    is also an important habitat for shorebirds such as sandpipers and gulls.
    </p>
    <p>
    Acadia National Park's unique combination of wildlife and plant diversity is a testament to the park's commitment to 
    conservation and preservation. The park's staff and volunteers work tirelessly to protect and restore the park's ecosystems, 
    ensuring that future generations can enjoy the park's natural beauty and biodiversity.
    </p>
    <p>
    In conclusion, Acadia National Park is a treasure trove of wildlife and plant diversity. The park's unique combination of 
    coastal and forest ecosystems provides a habitat for a range of animal and plant species, from bald eagles and moose to 
    lupines and seaweed. The park's commitment to conservation and preservation ensures that visitors can continue to enjoy the 
    park's natural beauty for years to come.
    </p>
    <div id="species">
      <h1 class="text-center">
        Types of Native Species Present in the Park
      </h1>
    </div>
  </div>
</template>

<script>
import species from './../../../assets/data/species_types_count.json'
import * as d3 from 'd3'

export default {
  mounted() {
      this.drawCharts()
    },
    beforeUnmount() {
      document.querySelector("#species > svg").remove()
    },
    methods: {
      drawCharts() {
        this.drawSpecies()
      },
      drawSpecies() {
        let margin = {left:50, rigth:20, top:20, bottom:30};
        let width = 800;
        let heigth = 400;

        let svg = d3.select("#species")
          .append("svg")
          .attr("viewBox", [0, 0, width + margin.left + margin.rigth, heigth + margin.top + margin.bottom])
          .style("background-color", "#F2E2CD")
          .append("g")
          .attr("transform", "translate(" + margin.left + "," + margin.top + ")");

        const x = d3.scaleBand()
                    .range([0, width])
                    .padding(0.2);
        x.domain(species.map((d) => d.type));
        const y = d3.scaleLinear()
                    .range([heigth, 0]);
        y.domain([0, 700]);

        const xAxis = d3.axisBottom(x)
        const yAxis = d3.axisLeft(y)

        svg.append("g")
          .attr("stroke", '#555358')
          .attr("transform", "translate(0," + heigth + ")")
          .call(xAxis);

        svg.append("g")
          .attr("stroke", '#555358')
          .call(yAxis);

        svg.selectAll(".bar")
          .data(species)
          .enter()
          .append("rect")
            .attr("class", "bar")
            .attr("x", (d) => x(d.type))
            .attr("y", (d) => y(d.count))
            .attr("width", x.bandwidth())
            .attr("height", (d) => heigth - y(d.count))
            .attr("fill", "#FF6666");

      }
    }

}
</script>

<style>

</style>