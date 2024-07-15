<script>
  import { scaleLinear } from "d3";
  import Scrolly from "./helpers/Scrolly.svelte";
  import initialStageData from "./assets/stage_results.json";
  import riders from "./assets/riders.json";
  import StepCount from "./components/StepCount.svelte";

  import YScale from "./components/YScale.svelte";

  let width;
  let height;

  const stageCount = Array(3);

  let renderedData = riders;
  let displayedResults;

  $: xScale = scaleLinear()
    .domain([0, 4])
    .range([40, width / 2 - 40]);

  $: yScale = scaleLinear()
    .domain([0, 130])
    .range([height - 150, 10]);

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
    }
  }

  // $: console.log(renderedData);
</script>

<div class="container">
  <div class="header"></div>
  <section>
    <div class="chart-container">
      <div class="chart" bind:clientWidth={width} bind:clientHeight={height}>
        <YScale {currentStep} {yScale} />
        <svg width="50vw" height="100vh" class="viz">
          {#each renderedData as rider}
            <circle
              cx={xScale(rider.rank)}
              cy={yScale(rider.time)}
              r="10"
              fill={rider.color}
            ></circle>
            <text
              dominant-baseline="middle"
              fill="white"
              x="20"
              y="0"
              transform="translate({xScale(rider.rank)},{yScale(
                rider.time
              )}) rotate(-90)">{rider.name}</text
            >
          {/each}
        </svg>
      </div>
      <StepCount {currentStep} {stageCount} {width} />
    </div>

    <Scrolly bind:value={currentStep}>
      {#each stageCount as stage, i}
        <div class="step step{i + 1}" class:active={currentStep === i}>
          <div class="step-content">
            Etape {i + 1}
          </div>
        </div>
      {/each}
    </Scrolly>
  </section>
  <!-- <div>END</div> -->
</div>

<style>
  .header {
    height: 100vh;
    width: 100vw;
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
    background-color: #615968;
  }

  circle {
    transition:
      cx 500ms ease,
      cy 1500ms ease;
  }

  .viz text {
    transition: transform 1500ms ease;
  }

  /* Scrollytelling CSS */
  .step {
    height: 150vh;
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
