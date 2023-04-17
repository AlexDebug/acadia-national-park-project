<template>
  <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
  <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
  <!-- <h1>{{ content }}</h1> -->
  <div id="app" class="flex flex-col mt-0">
    <IntroductionDiv/>
    <MainMapContentHandler />
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import MainMapContentHandler from './components/MapContentHandler.vue'
import IntroductionDiv from './components/IntroductionDiv.vue'
import content from './assets/static-text.json'

export default {
  name: 'App',
  components: {
    MainMapContentHandler,
    IntroductionDiv
  },
  data() {
    return {
      content:content
    }
  },
  mounted() {
        const observer = new IntersectionObserver(entries => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    console.log("visible");
                    entry.target.classList.add("show_from_view");
                }
                else {
                    entry.target.classList.remove("show_from_view");
                }
            });
        });
        const hiddenElement = document.querySelectorAll(".hidden_from_view");
        hiddenElement.forEach(element => {
          observer.observe(element);});
        }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Anton&family=Dancing+Script&family=Dongle:wght@700&family=DynaPuff:wght@400;500;700&family=Inspiration&family=Schibsted+Grotesk:ital,wght@0,400;1,800&family=Sedgwick+Ave+Display&display=swap');

#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  -webkit-user-select: none; /* Safari */
  -ms-user-select: none; /* IE 10 and IE 11 */
  user-select: none; /* Standard syntax */
  color: #555358;
  font-family: 'Dongle';
  font-size: 2rem;
  background: rgb(242,226,205);
  /* background: linear-gradient(180deg, rgba(242,226,205,1) 0%, rgba(240,235,225,1) 46%, rgba(235,223,215,1) 100%); */
}
/* make a media quiery for mobile on app id */
@media (max-width: 768px) {
  #app {
    font-size: 15px;
  }
}

.hidden_from_view{
    opacity: 0;
    filter: blur(5px);
    transform: translateX(-100%);
    transition: all 1s;
  }
.show_from_view {
    opacity: 1;
    filter: blur(0px);
    transform: translateX(0%);
  }
</style>
