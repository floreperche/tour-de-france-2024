<script>
  import { scaleLinear } from "d3";
  import Scrolly from "./helpers/Scrolly.svelte";
  import { forceSimulation, forceX, forceY, forceCollide } from "d3";
  import initialStageData from "./assets/stage_results.json";
  import riders from "./assets/riders.json";
  import StepCount from "./components/StepCount.svelte";
  import YScale from "./components/YScale.svelte";
  import Flat from "./components/Flat.svelte";
  import Hilly from "./components/Hilly.svelte";
  import Mountain from "./components/Mountain.svelte";
  import Rider from "./components/Rider.svelte";

  let width;
  let height;

  let renderedData = riders;
  let displayedResults;

  $: xScale = scaleLinear()
    .domain([0, 4])
    .range([40, width / 2 - 40]);

  $: yScale = scaleLinear()
    .domain([0, 130])
    .range([height - 150, 10]);

  let currentStep;

  let simulation = forceSimulation(renderedData);
  let nodes = [];
  simulation.on("tick", () => {
    nodes = simulation.nodes();
  });

  // $: {
  //   simulation
  //     .force(
  //       "x",
  //       forceX()
  //         .x((d) => xScale(d.rank))
  //         .strength(0.8)
  //     )
  //     .force(
  //       "y",
  //       forceY()
  //         .y((d) => yScale(d.time))
  //         .strength(0.1)
  //     )
  //     .force("collide", forceCollide().radius(10))
  //     .alpha(0.2)
  //     .alphaDecay(0.0005);
  // }

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

  // $: console.log(nodes);
</script>

<div class="container">
  <div class="header"></div>
  <section>
    <div class="chart-container">
      <div class="chart" bind:clientWidth={width} bind:clientHeight={height}>
        <YScale {currentStep} {yScale} />
        <svg
          width="50vw"
          height="100vh"
          class="viz"
          style="background-color : {currentStep + 1 === 9
            ? '#E5E1D5'
            : '#615968'}"
        >
          {#each renderedData as rider}
            <ellipse
              cx={xScale(rider.rank)}
              cy={yScale(rider.time)}
              rx="6.40862"
              ry="0.610345"
              fill="black"
            />
            <ellipse
              cx={xScale(rider.rank)}
              cy={yScale(rider.time)}
              rx="0.610345"
              ry="8.4431"
              fill="#121313"
            />
            <ellipse
              cx={xScale(rider.rank)}
              cy={yScale(rider.time)}
              rx="1.01724"
              ry="3.3569"
              fill="#488836"
            />
            <ellipse
              cx={xScale(rider.rank)}
              cy={yScale(rider.time) - 42.12}
              rx="0.610345"
              ry="8.4431"
              fill="#121313"
            />
            <ellipse
              cx={xScale(rider.rank)}
              cy={yScale(rider.time) - 42.12}
              rx="1.01724"
              ry="3.3569"
              fill="#121313"
            />
            <ellipse
              cx={xScale(rider.rank) + 4.07}
              cy={yScale(rider.time) - 12.72}
              rx="0.610345"
              ry="13.4276"
              fill="#BC7863"
            />
            <ellipse
              cx={xScale(rider.rank) - 4.07}
              cy={yScale(rider.time) - 12.72}
              rx="0.610345"
              ry="13.4276"
              fill="#BC7863"
            />
            <ellipse
              cx={xScale(rider.rank)}
              cy={yScale(rider.time) - 22.79}
              rx="5.08621"
              ry="10.4776"
              fill={rider.color}
            />
            <circle
              cx={xScale(rider.rank)}
              cy={yScale(rider.time) - 12.11}
              r="2.84828"
              fill="#121313"
            />

            <!-- <Rider {rider} /> -->
            <!-- {#if currentStep >= 0}
              <text
                dominant-baseline="middle"
                fill="white"
                x="20"
                y="0"
                transform="translate({xScale(rider.rank)},{yScale(
                  rider.time
                )}) rotate(-90)"
              >
                {rider.name}</text
              >=
            {/if} -->
          {/each}
        </svg>
      </div>
      <StepCount {currentStep} stageCount={initialStageData} {width} />
    </div>

    <Scrolly bind:value={currentStep}>
      {#each initialStageData as stage, i}
        <div class="step step{i + 1}" class:active={currentStep === i}>
          {#if stage.type === "flat"}
            <Flat {width} {height} curentStage={stage.id} {initialStageData} />
          {:else if stage.type === "hilly"}
            <Hilly
              {width}
              {height}
              curentStage={stage.id}
              {initialStageData}
            />{:else if stage.type === "mountain"}
            <Mountain
              {width}
              {height}
              curentStage={stage.id}
              {initialStageData}
            />{/if}
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
    transition: background-color 800ms ease;
  }

  ellipse,
  circle {
    transition:
      cx 500ms ease,
      cy 1500ms ease;
  }

  /* Scrollytelling CSS */
  .step {
    height: 150vh;
    width: 25vw;
    display: flex;
    place-items: center;
    justify-content: center;
    margin-left: auto;
    margin-right: 0;
  }
</style>
