<template>
    <div id="Handler" class="flex flex-col items-center pb-[25%] w-100 space-y-5">
        <MainMap @feature-clicked="contentHandler"/>
        <FeaturesDescription :feature="feature" @feature_type="featuretypeHandler"/>
        <div>
            <input
                v-model="show_spheres"
                v-if="show_toggle"
                class="mr-2 mt-[0.3rem] h-3.5 w-8 appearance-none rounded-[0.4375rem] bg-neutral-300 before:pointer-events-none before:absolute before:h-3.5 before:w-3.5 before:rounded-full before:bg-transparent before:content-[''] after:absolute after:z-[2] after:-mt-[0.1875rem] after:h-5 after:w-5 after:rounded-full after:border-none after:bg-neutral-100 after:shadow-[0_0px_3px_0_rgb(0_0_0_/_7%),_0_2px_2px_0_rgb(0_0_0_/_4%)] after:transition-[background-color_0.2s,transform_0.2s] after:content-[''] checked:bg-primary checked:after:absolute checked:after:z-[2] checked:after:-mt-[3px] checked:after:ml-[1.0625rem] checked:after:h-5 checked:after:w-5 checked:after:rounded-full checked:after:border-none checked:after:bg-primary checked:after:shadow-[0_3px_1px_-2px_rgba(0,0,0,0.2),_0_2px_2px_0_rgba(0,0,0,0.14),_0_1px_5px_0_rgba(0,0,0,0.12)] checked:after:transition-[background-color_0.2s,transform_0.2s] checked:after:content-[''] hover:cursor-pointer focus:outline-none focus:ring-0 focus:before:scale-100 focus:before:opacity-[0.12] focus:before:shadow-[3px_-1px_0px_13px_rgba(0,0,0,0.6)] focus:before:transition-[box-shadow_0.2s,transform_0.2s] focus:after:absolute focus:after:z-[1] focus:after:block focus:after:h-5 focus:after:w-5 focus:after:rounded-full focus:after:content-[''] checked:focus:border-primary checked:focus:bg-primary checked:focus:before:ml-[1.0625rem] checked:focus:before:scale-100 checked:focus:before:shadow-[3px_-1px_0px_13px_#3b71ca] checked:focus:before:transition-[box-shadow_0.2s,transform_0.2s] dark:bg-neutral-600 dark:after:bg-neutral-400 dark:checked:bg-primary dark:checked:after:bg-primary dark:focus:before:shadow-[3px_-1px_0px_13px_rgba(255,255,255,0.4)] dark:checked:focus:before:shadow-[3px_-1px_0px_13px_#3b71ca]"
                type="checkbox"
                role="switch"
                id="flexSwitchCheckDefault" />
            <label v-if="show_toggle"
            class="inline-block pl-[0.15rem] 
                hover:cursor-pointer"
            for="flexSwitchCheckDefault">
            Toggle for more info about {{ this.feature.type }}</label>
        </div>
        <div v-if="show_spheres">
            <GeoSphere v-if="this.feature_type === 'geosphere'" />
            <HidroSphere v-if="this.feature_type === 'hidrosphere'"/>
            <AtmoSphere v-if="this.feature_type == 'atmosphere'" />
            <BiosSphere v-if="this.feature_type === 'biosphere'"/>
        </div>
    </div>
</template>

<script>
import MainMap from "./MainMap.vue";
import FeaturesDescription from "./FeatureDescription.vue";

import BiosSphere from "./static-text/spheres/BiosSphere.vue";
import AtmoSphere from "./static-text/spheres/AtmoSphere.vue";
import GeoSphere from "./static-text/spheres/GeoSphere.vue";
import HidroSphere from "./static-text/spheres/HidroSphere.vue";

export default {
    name: "MapContentHandler",
    components: {
        MainMap,
        FeaturesDescription,

        BiosSphere,
        AtmoSphere,
        GeoSphere,
        HidroSphere,
    },
    data() {
        return {
            feature: "No feature selected",
            feature_type: null,
            show_toggle: false,
            show_spheres: false,
        }
    },
    methods: {
        contentHandler: function (e) {
            this.feature = e;
            this.show_toggle = true;
        },
        featuretypeHandler (e) {
            this.feature_type = e;
        }
    }

}
</script>