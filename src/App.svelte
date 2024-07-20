<script>
  import { scaleLinear } from "d3";
  import Scrolly from "./helpers/Scrolly.svelte";
  import initialStageData from "./assets/stage_results.json";
  import riders from "./assets/riders.json";
  import Header from "./components/Header.svelte";
  import YScale from "./components/YScale.svelte";
  import Flat from "./components/landscapes/Flat.svelte";
  import Hilly from "./components/landscapes/Hilly.svelte";
  import Mountain from "./components/landscapes/Mountain.svelte";
  import Rider from "./components/Rider.svelte";
  import ItalianLandscape from "./components/landscapes/ItalianLandscape.svelte";
  import NiceLandscape from "./components/landscapes/NiceLandscape.svelte";
  import Footer from "./components/Footer.svelte";

  let width;
  let height;
  let renderedData;
  let displayedResults;
  let maxYScale = 130;
  let curentStep;

  // Scales
  $: xScale = scaleLinear()
    .domain([0, 4])
    .range([5, width / 2 - 15]);

  $: heightMargin = height && height < 576 ? 40 : 80;

  $: yScale = scaleLinear()
    .domain([0, maxYScale])
    .range([height - heightMargin, 10]);

  // Data
  $: {
    if (curentStep === undefined) {
      renderedData = riders;
    } else {
      initialStageData.map((e) => {
        if (e.id === curentStep + 1) {
          displayedResults = e.riders;
        }
      });
      renderedData = riders.map((obj, i) => {
        return {
          ...obj,
          stage: curentStep + 1,
          rank: displayedResults[i].rank,
          time: displayedResults[i].time,
        };
      });
      if (curentStep > 11) {
        maxYScale = 500;
      } else {
        maxYScale = 130;
      }
    }
  }
</script>

<div class="background">
  <div
    class="container"
    style="background-color:{curentStep + 1 === 9 ? '#F2F2E3' : '#615968'}"
  >
    <!-- Managing initial landscape -->
    <div class="initial-landscape" style="height: {height}px">
      <ItalianLandscape {width} {height} {curentStep} />
    </div>

    <!-- Header -->
    <Header />

    <!-- Core visualisation -->
    <section>
      <!-- Chart -->
      <div class="chart-container">
        <div class="chart" bind:clientWidth={width} bind:clientHeight={height}>
          <YScale {curentStep} {maxYScale} {height} {heightMargin} />
          <svg width={width * 0.75} {height} class="viz">
            <line
              x1={width / 2 - 10}
              x2={width / 2 - 10}
              y1={0}
              y2={height}
              stroke="white"
              stroke-width="3"
              opacity="0.5"
            ></line>

            {#each renderedData as rider}
              {#if !isNaN(xScale(rider.rank)) && !isNaN(yScale(rider.time))}
                <Rider {rider} {xScale} {yScale} {curentStep} {height} />{/if}
            {/each}
          </svg>
        </div>
      </div>

      <!-- Scrolly animation -->
      <Scrolly bind:value={curentStep}>
        {#each initialStageData as stage, i}
          <div class="step step{i + 1}" class:active={curentStep === i}>
            <!-- Managing types of landscapes -->
            {#if stage.type === "final"}
              <NiceLandscape {width} {height} {curentStep} />
            {:else if stage.type === "flat"}
              <Flat
                {width}
                {height}
                curentStage={stage.id}
                {curentStep}
                {initialStageData}
              />
            {:else if stage.type === "hilly"}
              <Hilly
                {width}
                {height}
                curentStage={stage.id}
                {curentStep}
                {initialStageData}
              />{:else if stage.type === "mountain"}
              <Mountain
                {width}
                {height}
                curentStage={stage.id}
                {curentStep}
                {initialStageData}
              />{/if}
          </div>
        {/each}
      </Scrolly>
    </section>

    <!-- Displaying result -->
    <div class="result">
      <svg {width} height={width * 0.3}>
        <line
          x1={width * (3 / 4) - 10}
          x2={width * (3 / 4) - 10}
          y1="0"
          y2="100%"
          stroke="white"
          stroke-width="3"
          opacity="0.5"
        ></line>
        <g transform="translate({width / 2},  0) scale({width / 320})">
          <text
            x="0"
            y="40"
            fill="white"
            text-anchor="middle"
            dominant-baseline="end"
            font-size="38"
            opacity="0.5">XXXXXXX</text
          >
          <text
            x="0"
            y="80"
            fill="white"
            text-anchor="middle"
            font-size="38"
            opacity="0.5">WINS!</text
          >
        </g>
      </svg>
    </div>

    <!-- Footer -->
    <Footer />
  </div>
</div>

<style>
  .background {
    background-color: #403b44;
  }
  .container {
    position: relative;
    max-width: 700px;
    box-shadow: 0px 10px 20px rgb(30, 29, 32);
    margin: 0 auto;
    transition: all 1000ms ease;
  }
  .initial-landscape {
    position: absolute;
    width: 100%;
    top: 100vh;
    right: 0;
  }

  .chart-container {
    position: sticky;
    width: 100%;
    top: 0%;
  }

  .chart {
    width: 100%;
    height: 100vh;
    display: flex;
  }
  .viz {
    transition: background-color 800ms ease;
  }

  /* Scrollytelling CSS */
  .step {
    height: 125vh;
    width: 100%;
    display: flex;
    place-items: center;
    justify-content: end;
    margin-left: auto;
    margin-right: 0;
  }

  .result {
    font-family: "Caveat Brush", cursive;
  }
</style>
