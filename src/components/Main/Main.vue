<script setup lang="ts">
import { ref } from 'vue';

const pageViews = ref<number>(100);
const pricing = ref(16);

</script>

<template>
    <div id="numbers">
        <h2>{{ pageViews }}K Pageviews</h2>
        <div id="pricing">
            <span>${{ pricing.toFixed(2) }}</span> /month
        </div>
    </div>
    <input id="page-views-range" type="range" title="Page views range">

    Monthly Billing
    Yearly Billing 25% discount

    Unlimited websites
    100% data ownership
    Email reports

    Start my trial
</template>

<style scoped>
#page-views-range {
    appearance: none;
    display: block;
    width: 100%;
}
    #page-views-range:hover {
        cursor: pointer;
    }

    #page-views-range::-webkit-slider-thumb {
        /* background-image: url(../../assets/images/icon-slider.svg); */
        background-color: white;
    }
    #page-views-range::-moz-range-thumb {
        background-color: white;
    }
</style>