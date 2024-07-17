<script>
  import { scaleLinear } from "d3";
  import Scrolly from "./helpers/Scrolly.svelte";
  import initialStageData from "./assets/stage_results.json";
  import riders from "./assets/riders.json";
  import Header from "./components/Header.svelte";
  import YScale from "./components/YScale.svelte";
  import Flat from "./components/Flat.svelte";
  import Hilly from "./components/Hilly.svelte";
  import Mountain from "./components/Mountain.svelte";
  import Rider from "./components/Rider.svelte";

  let width;
  let height;

  let renderedData = riders;
  let displayedResults;

  let maxYScale = 130;

  $: xScale = scaleLinear()
    .domain([0, 4])
    .range([20, width / 2 - 20]);

  $: yScale = scaleLinear()
    .domain([0, maxYScale])
    .range([height - 100, 10]);

  let currentStep;

  $: {
    if (currentStep === undefined) {
      renderedData = riders;
    } else {
      initialStageData.map((e) => {
        if (e.id === currentStep + 1) {
          displayedResults = e.riders;
        }
      });
      renderedData = riders.map((obj, i) => {
        return {
          ...obj,
          rank: displayedResults[i].rank,
          time: displayedResults[i].time,
        };
      });
      if (currentStep > 11) {
        maxYScale = 560;
      } else {
        maxYScale = 130;
      }
    }
  }
</script>

<div class="container" style="position: relative">
  <div class="initial-landscape"></div>
  <Header />

  <section>
    <div class="chart-container">
      <div class="chart" bind:clientWidth={width} bind:clientHeight={height}>
        <YScale {currentStep} {maxYScale} {height} />
        <svg width="50vw" height="100vh" class="viz">
          <line
            x1={width / 2 - 14}
            x2={width / 2 - 14}
            y1={0}
            y2={height}
            stroke="white"
            stroke-width="3"
            opacity="0.5"
          ></line>
          {#each renderedData as rider}
            <Rider {rider} {xScale} {yScale} {currentStep} />
          {/each}
        </svg>
      </div>
      <!-- <StepCount {currentStep} stageCount={initialStageData} {width} /> -->
    </div>

    <Scrolly bind:value={currentStep}>
      {#each initialStageData as stage, i}
        <div class="step step{i + 1}" class:active={currentStep === i}>
          {#if stage.type === "flat"}
            <Flat
              {width}
              {height}
              curentStage={stage.id}
              {currentStep}
              {initialStageData}
            />
          {:else if stage.type === "hilly"}
            <Hilly
              {width}
              {height}
              curentStage={stage.id}
              {currentStep}
              {initialStageData}
            />{:else if stage.type === "mountain"}
            <Mountain
              {width}
              {height}
              curentStage={stage.id}
              {currentStep}
              {initialStageData}
            />{/if}
        </div>
      {/each}
    </Scrolly>
  </section>

  <!-- <div>END</div> -->
</div>

<style>
  .initial-landscape {
    position: absolute;
    width: 25vw;
    height: 100vh;
    top: 100vh;
    right: 0;
    background: linear-gradient(#615968 85%, #609978);
  }
  .container {
    background-color: #615968;
  }

  .chart-container {
    position: sticky;
    width: 100vw;
    height: 100vh;
    top: 0%;
  }

  .chart {
    width: 100vw;
    position: relative;
    display: flex;
  }
  .viz {
    transition: background-color 800ms ease;
  }

  /* Scrollytelling CSS */
  .step {
    height: 150vh;
    width: 100vw;
    display: flex;
    place-items: center;
    justify-content: end;
    margin-left: auto;
    margin-right: 0;
  }
</style>
