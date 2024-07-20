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
  import ItalianLandscape from "./components/ItalianLandscape.svelte";
  import NiceLandscape from "./components/NiceLandscape.svelte";

  let width;
  let height;
  let renderedData;
  let displayedResults;
  let maxYScale = 130;
  let curentStep;

  $: xScale = scaleLinear()
    .domain([0, 4])
    .range([5, width / 2 - 15]);

  $: heightMargin = height && height < 576 ? 40 : 80;

  $: yScale = scaleLinear()
    .domain([0, maxYScale])
    .range([height - heightMargin, 10]);

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
    style="position: relative; background-color:{curentStep + 1 === 9
      ? '#F2F2E3'
      : '#615968'}"
  >
    <div class="initial-landscape" style="height: {height}px">
      <ItalianLandscape {width} {height} {curentStep} />
    </div>
    <Header />

    <section>
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
                <Rider {rider} {xScale} {yScale} {curentStep} />{/if}
            {/each}
          </svg>
        </div>
      </div>

      <Scrolly bind:value={curentStep}>
        {#each initialStageData as stage, i}
          <div class="step step{i + 1}" class:active={curentStep === i}>
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

    <div class="footer">
      <div>
        <p>A project designed and developed by</p>
        <div>
          <a href="https://www.wildvariables.com" target="_blank"
            ><img
              src="src\assets\visuals\logo_wv_png.png"
              alt="logo Wild Variables"
            /></a
          >
        </div>
      </div>
      <p>
        Source: <a href="https://www.letour.fr/fr/" target="_blank"
          >www.letour.fr</a
        >
        •
        <a
          href="https://github.com/wildvariables/tour-de-france-2024"
          target="_blank">See the code</a
        >
      </p>
    </div>
  </div>
</div>

<style>
  .background {
    background-color: #403b44;
  }
  .container {
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

  .footer {
    color: white;
    background-color: #504c53;
    padding: 40px 20px;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 20px;
    text-align: center;
  }

  .footer div {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 10px;
  }

  .footer a {
    color: white;
    text-align: center;
    display: inline-table;
    position: relative;
  }

  .footer img {
    width: 120px;
  }
</style>
