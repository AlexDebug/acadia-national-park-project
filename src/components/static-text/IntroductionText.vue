<template>
  <div class="space-y-5 text-left px-[15%] pb-[5%]" id="introduction_text">
    <section id="introduction_headings" class="hidden_from_view mt-[50vh]">
      <h1 class="text-center"><strong>Welcome to Acadia National Park</strong></h1>
      <h3 class="text-center"><em>A breathtakingly beautiful natural area</em></h3>
    </section>
    <section class="hidden_from_view">
      <img src="https://www.nps.gov/npgallery/GetAsset/59BF74FE-1DD8-B71B-0B12236677EC68A4/proxy/hires?" class="w-[100%] mb-[5vh]">
      <p>
      Nestled on the coast of Maine in the Northeastern region of the United States, Acadia National Park is a natural wonder 
      that offers a diverse range of landscapes, ecosystems, and habitats. The park is home to over 49,000 acres of rugged 
      coastlines, granite peaks, dense forests, and pristine lakes, attracting millions of visitors every year. Acadia National 
      Park is not just a beautiful destination for tourists but a natural laboratory that highlights the interconnectedness of 
      the four spheres of Earth's environment - Geosphere, Hydrosphere, Biosphere, and Atmosphere.
      </p>
    </section>
    <div></div>
      <section class="hidden_from_view min-h-[100vh]">
        <p>
        The Geosphere of Acadia National Park boasts an impressive collection of geological formations that reflect millions of 
        years of Earth's history. The park's granite peaks, rocky coastlines, and glacial moraines are testaments to the dynamic 
        forces that shaped the land over time. Mount Desert Island, the park's largest landmass, features unique landforms such as
         Cadillac Mountain, the highest point on the US Atlantic coast, and Jordan Pond, a beautiful glacial lake that reflects 
         the surrounding mountains.
        </p>
        <p>
        The Hydrosphere of Acadia National Park is equally impressive, featuring a diverse range of aquatic habitats that 
        support a wide variety of life. The park is home to numerous freshwater lakes, streams, and ponds, as well as the  
        Atlantic Ocean, which borders the park on three sides. The marine ecosystem of Acadia is home to a rich diversity of 
        species, including seals, whales, dolphins, and various types of fish and shellfish.
        </p>
        <p>
        The Biosphere of Acadia National Park is a vast and intricate network of ecosystems that support an abundance of plant 
        and animal life. The park is home to over 2,000 different species of plants, ranging from coastal heaths to boreal 
        forests. The wildlife in the park is equally impressive, with over 40 species of mammals, including black bears, moose, 
        and red foxes, as well as more than 270 species of birds.
        </p>
        <p>
        Finally, the Atmosphere of Acadia National Park is dynamic and ever-changing, influenced by the surrounding landscape, 
        ocean, and weather patterns. Visitors to the park can experience a wide range of weather conditions, 
        from warm, sunny days to cold, snowy winters. The park is also home to unique weather events, 
        such as the "Indian Summer" phenomenon, where warm temperatures and bright foliage mark the onset of autumn.
        </p>
      </section>
      <div></div>
      <section class="hidden_from_view flex flex-col items-center">
        <p>
        In conclusion, Acadia National Park is a natural wonder that showcases the intricate relationships between the four 
        spheres of Earth's environment. The park's unique geology, diverse aquatic habitats, rich biodiversity, and dynamic 
        atmosphere make it a must-visit destination for nature lovers and scientists alike.
        </p>
        <h1 id="go_to_map" v-on:click="moveBar">GO TO MAP</h1>
    </section>
    
  </div>
</template>

<script>

export default {
    name: "IntroductionText",
    methods: {
        moveBar: function () {
          document.getElementById("mapContainer").scrollIntoView();
        }
    }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Anton&family=Dancing+Script&family=Dongle:wght@700&family=DynaPuff:wght@400;500;700&family=Inspiration&family=Schibsted+Grotesk:ital,wght@0,400;1,800&family=Sedgwick+Ave+Display&display=swap');

  #introduction_text{
    font-family: "Dongle";
    /* font-size: 1.5rem; */
  }

  #introduction_text > *{
    min-height: 100vh;
  }

  #introduction_text > div{
    min-height: 50vh;
  }

  #introduction_headings > h1{
    /* font-family: "DynaPuff"; */
    font-size: 5rem;
  }
  @media (max-width: 768px) {
    #introduction_headings > h1{
      font-size: 3rem;
    }
    #go_to_map {
      font-size: 1rem;
    }
  }

  #introduction_headings > h3{
    font-family: "DynaPuff";
    font-size: 1rem;
  }

  #go_to_map {

        text-align: center;
        font-family: 'Dancing Script', bold;
        inline-size: 25vw;
        font-size: 2rem;
        font-weight: 900;
        text-shadow: 0 0 10px #534f49;
        padding: 2vh 1vw;
        z-index: 1;
    }

    #go_to_map:hover {
        transition: background-color 0.5s, 
                    backdrop-filter 0.5s, 
                    border-width 0.5s, border-color 0.5s, 
                    box-shadow 0.5s, 
                    border-radius 0.5s;
        text-shadow: 10px 10px 10px #534f49;
        background-color: rgba(240, 235, 225, 0.2);
        backdrop-filter: blur(20px);
        border-width: 4px;
        border-color: rgba(240, 235, 225, 0.5);
        box-shadow: 4px 4px 10px #534f49;
    }
        
</style>