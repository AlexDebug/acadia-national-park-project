<template>
    <div class="space-y-5 text-left px-[15%] pb-[5%]">
        <img :src="image" class="w-[100%] h-[75vh]">
        <h1 v-if="this.show">{{ content }}</h1>
    </div>
</template>

<script>
import features from "./../assets/features.json";

export default {
    name: "FeatureDescription",
    props: {
        feature: null,
    },
    emits: ['feature_type'],
    data() {
        return {
            show: false,
            content: null,
            image: null,
        }
    },
    watch: {
        feature: function (newVal) {
            this.show = true;
            switch(newVal.type) {
                case "Geosphere": {
                    features.Geosphere.find((element) => {
                        if (element.name === newVal.name) {
                            this.content = element.description;
                            this.image = element.image;
                        }
                    });
                    this.$emit("feature_type", "geosphere");
                    break;
                }
                case "Hidrosphere": {
                    features.Hidrosphere.find((element) => {
                        if (element.name === newVal.name) {
                            this.content = element.description;
                            this.image = element.image;
                        }
                    });
                    this.$emit("feature_type", "hidrosphere");
                    break;
                }
                case "Atmosphere": {
                    features.Atmosphere.find((element) => {
                        if (element.name === newVal.name) {
                            this.content = element.description;
                            this.image = element.image;
                        }
                    });
                    this.$emit("feature_type", "atmosphere");
                    break;
                }
                case "Biosphere": {
                    features.Biosphere.find((element) => {
                        if (element.name === newVal.name) {
                            this.content = element.description;
                            this.image = element.image;
                        }
                    });
                    this.$emit("feature_type", "biosphere");
                    break;
                }
            }
        }
    }
}
</script>