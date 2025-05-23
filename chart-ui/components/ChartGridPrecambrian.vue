<script setup lang="ts">
import { type chartNode, type scalingFactor } from "@/utils/util"


const props = defineProps<{
    node: chartNode,
    lang: string,
    scaling: scalingFactor
}>()

const emit = defineEmits<{
    (e: 'view', node: string): void
}>()

</script>
<template>
     <div class="grid-wrapper">
        <div class="grid-5 precambrian-grid">
            <div class="header v-text">Super Eon</div>
            <div class="header v-text">Eon</div>
            <div class="header">Era</div>
            <div class="header">Period
                <span class="v-text gssp-text ">GSSP / GSSA</span>
            </div>
            <div class="header">Numeric Age</div>
            <ChartGridPrecambrianCell :lang="props.lang" :node="props.node" :parent-rank="''" :scaling="props.scaling"
                @view="x => emit('view', x)" />
        </div>
        <div class="chart-notes">
            <p>Units of all ranks are in the process of being defined by Global Boundary
                Stratotype Section and Points (GSSP) for their lower boundaries, including
                those of the Archean and Proterozoic, long defined by Global Standard
                Stratigraphic Ages (GSSA). Italic fonts indicate informal units and
                placeholders for unnamed units. Versioned charts and detailed information
                on ratified GSSPs are available at the website http://www.stratigraphy.org.
                The URL to this chart is found below.</p>
            <p>
                Numerical ages are subject to revision and do not define units in the
                Phanerozoic and the Ediacaran; only GSSPs do. For boundaries in the
                Phanerozoic without ratified GSSPs or without constrained numerical
                ages, an approximate numerical age (~) is provided.</p>
            <p>
                Ratified Subseries/Subepochs are abbreviated as U/L (Upper/Late), M
                (Middle) and L/E (Lower/Early). Numerical ages for all systems except
                Quaternary, upper Paleogene, Cretaceous, Jurassic, Triassic, Permian,
                Cambrian and Precambrian are taken from ‘A Geologic Time Scale
                2012’ by Gradstein et al. (2012), those for the Quaternary, upper
                Paleogene, Cretaceous, Jurassic, Triassic, Permian, Cambrian and
                Precambrian were provided by the relevant ICS subcommissions.</p>
        </div>
    </div>
</template>
<style scoped>
.grid-5 {
    margin-top: 4rem;
    --_thin-col: 2rem;
    --_mid-col: 6fr;
    display: grid;
    grid-template-columns:
        repeat(2, var(--_thin-col)) repeat(3, var(--_wide-col, 1fr));
    /* font-size: 0.6em; */
}

.header {
    position: relative;
    /* width: 100%; */
    /* margin-bottom:-1rem; */
}
div.header:not(.v-text){
    padding-left:5px;
}
.col-span-2 {
    grid-column: span 2;
}
.grid-5 :deep(div:last-child>.num-age-beginning){
    display:block;
    transform: translate(-50%,50%);
    bottom: 0px;
}

.v-text {
    display: inline-block;
    transform-origin: 0 0;
    transform: rotate(-90deg)
}

.gssp-text {
    position: absolute;
    right: 0rem;
    bottom: 0;
    transform-origin: 0 0;
    transform: rotate(-90deg) translateY(400%);
    word-break: normal;
    /* font-size: 0.8em;; */
}

@media print {
    p {
        font-size: 0.6em;
    }
}
</style>