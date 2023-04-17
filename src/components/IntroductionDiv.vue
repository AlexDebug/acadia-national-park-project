<template>
  <div class="flex flex-col w-[100%] items-center">
    <IntroductionHeader />
    <IntroductionText />
  </div>
</template>

<script>
import IntroductionText from './static-text/IntroductionText.vue';
import IntroductionHeader from './IntroductionHeader.vue';

export default {
    name: "IntroductionDiv",
    components : {
        IntroductionText,
        IntroductionHeader
    }
}
</script>

<style>

</style>