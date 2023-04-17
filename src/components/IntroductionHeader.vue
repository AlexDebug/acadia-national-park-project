<template>
    
    <section>
        <h1 id="image_text" v-on:click="moveBar">START TRIP</h1>
        <div class="flex flex-row m-0 w-[100vw] h-[100vh]" id="header_images">
            <!-- <img src="./../assets/header/poster_1.jpg" /> -->
            <!-- <img src="./../assets/header/poster_2.jpg" /> -->
            <img src="./../assets/header/poster_3.jpg" />
            <img src="./../assets/header/poster_4.jpg" />
            <!-- <img src="./../assets/header/poster_5.jpg" /> -->
            <img src="./../assets/header/poster_6.jpg" />
        </div>
        
        
    </section>
</template>

<script>

export default {
    name: "IntroductionHeader",
    methods: {
        moveBar: function () {
            window.scrollTo(0, window.innerHeight);
        }
    }
}
</script>

<style>
    @import url('https://fonts.googleapis.com/css2?family=Anton&family=Dancing+Script&family=DynaPuff:wght@400;500;700&family=Inspiration&family=Schibsted+Grotesk:ital,wght@0,400;1,800&family=Sedgwick+Ave+Display&display=swap');
    

    img {
        transition: filter 60s;
        width: 33.33333333%;
        height: 100vh;
        object-fit: cover;
        filter: grayscale(50%);
    }
    #image_text {
        font-family: 'Dancing Script', bold;
        inline-size: 50vw;
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        color: #F2E2CD;
        font-size: 5rem;
        font-weight: 900;
        text-shadow: 0 0 10px #534f49;
        padding: 2vh 1vw;
        z-index: 1;
    }

    #image_text:hover {
        transition: background-color 0.5s, 
                    backdrop-filter 0.5s, 
                    border-width 0.5s, border-color 0.5s, 
                    box-shadow 0.5s, 
                    border-radius 0.5s;
        text-shadow: 10px 10px 10px #534f49;
        background-color: rgba(240, 235, 225, 0.2);
        backdrop-filter: blur(10px);
        border-width: 4px;
        border-color: rgba(240, 235, 225, 0.5);
        box-shadow: 4px 4px 10px #534f49;
        border-radius: 10px;
    }

    #image_text:hover + #header_images > img{
        transition: filter 1s;
        filter: blur(1px) grayscale(50%);
        /* backdrop-filter: blur(10px); */
    }

    @media (max-width: 768px) {
        #image_text {
            font-size: 3rem;
        }
    }
</style>