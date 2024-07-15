<script>
  import { scaleLinear } from "d3";
  import Scrolly from "./helpers/Scrolly.svelte";
  import initialStageData from "./assets/stage_results.json";

  let width;
  let height;

  // console.log(initialStageData[0].riders);

  let randeredStageData = initialStageData[0].riders;

  // let randeredData = data

  $: xScale = scaleLinear()
    .domain([0, 4])
    .range([40, width - 40]);

  $: yScale = scaleLinear()
    .domain([0, 100])
    .range([height - 150, 10]);

  let currentStep;

  $: {
    if (currentStep === undefined) {
      randeredStageData = initialStageData[0].riders;
    } else {
      initialStageData.map((stage) => {
        if (stage.id === currentStep + 1) {
          randeredStageData = stage.riders;
        }
      });
    }
  }
</script>

<div class="container">
  <div class="header"></div>
  <section>
    <div class="chart" bind:clientWidth={width} bind:clientHeight={height}>
      <div class="position: relative">
        <svg width="50vw" height="100vh">
          {#each randeredStageData as rider}
            <circle
              cx={xScale(rider.rank)}
              cy={yScale(rider.time)}
              r="20"
              fill="white"
            ></circle>
          {/each}
        </svg>
        {#if currentStep >= 0}
          <div class="stage">
            Etape {currentStep + 1}
          </div>
        {/if}
      </div>
    </div>

    <Scrolly bind:value={currentStep}>
      {#each [1, 2, 3] as text, i}
        <div class="step step{text}" class:active={currentStep === i}>
          <div class="step-content">
            Etape {text}
          </div>
        </div>
      {/each}
    </Scrolly>
  </section>
  <div>END</div>
</div>

<style>
  .header {
    height: 100vh;
    width: 100vw;
    background-color: #5c5c5c;
  }

  .chart {
    background: lightblue;
    width: 50vw;
    height: 100vh;
    position: sticky;
    top: 0%;
    margin: auto;
  }

  svg {
    background-color: #5c5c5c;
  }

  .stage {
    position: absolute;
    bottom: 50px;
    left: 10px;
  }

  circle {
    transition:
      cx 2000ms ease,
      cy 2000ms ease;
  }

  /* Scrollytelling CSS */
  .step {
    height: 120vh;
    width: 25vw;
    display: flex;
    place-items: center;
    justify-content: center;
    background-color: #478692;
    margin-left: auto;
    margin-right: 0;
  }

  .step1 {
    background-color: #9cd067;
  }

  .step2 {
    background-color: #609978;
  }
</style>
