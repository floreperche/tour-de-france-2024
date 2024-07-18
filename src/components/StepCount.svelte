<script>
  export let currentStep;
  export let stageCount;
  export let width;
  import { scaleLinear } from "d3";

  //   $: console.log(stageScale(2));

  $: stageScale = scaleLinear()
    .domain([1, stageCount.length])
    .range([30, width - 30]);
</script>

<div class="step-counter">
  {#if currentStep >= 0}
    <p class="stage">Etape {currentStep + 1}</p>
    <svg {width}>
      {#each stageCount as stage, i}
        <circle
          cx={stageScale(i + 1)}
          cy="30"
          r="5"
          fill={i <= currentStep ? "white" : "grey"}
        />{/each}
    </svg>
  {/if}
</div>

<style>
  .step-counter {
    position: absolute;
    bottom: 0%;
    width: 100vw;
    height: 80px;
    background: linear-gradient(transparent, #615968);
    color: #ffffff;
  }

  .step-counter p {
    text-align: center;
  }
</style>
