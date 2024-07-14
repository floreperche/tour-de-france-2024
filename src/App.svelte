<script>
  import { scaleLinear } from "d3";
  import Scrolly from "./helpers/Scrolly.svelte";

  let width;
  let height;

  let data = [
    { rank: 2, time: 100, color: "yellow" },
    { rank: 2, time: 100, color: "black" },
    { rank: 2, time: 100, color: "blue" },
  ];

  // let randeredData = data

  $: xScale = scaleLinear()
    .domain([1, 3])
    .range([40, width - 40]);

  $: yScale = scaleLinear()
    .domain([0, 100])
    .range([height - 150, 10]);

  let currentStep;

  $: console.log(currentStep);

  $: {
    if (currentStep === undefined) {
      data = [
        { rank: 2, time: 100, color: "yellow" },
        { rank: 2, time: 100, color: "black" },
        { rank: 2, time: 100, color: "blue" },
      ];
    }
    if (currentStep === 0) {
      data = [
        { rank: 1, time: 0, color: "yellow" },
        { rank: 2, time: 20, color: "black" },
        { rank: 3, time: 50, color: "blue" },
      ];
    } else if (currentStep === 1) {
      data = [
        { rank: 1, time: 0, color: "yellow" },
        { rank: 2, time: 40, color: "black" },
        { rank: 3, time: 90, color: "blue" },
      ];
    } else if (currentStep === 2) {
      data = [
        { rank: 2, time: 30, color: "yellow" },
        { rank: 1, time: 0, color: "black" },
        { rank: 3, time: 200, color: "blue" },
      ];
    }
  }
</script>

<div class="container">
  <div class="header"></div>
  <section>
    <div class="chart" bind:clientWidth={width} bind:clientHeight={height}>
      <div class="position: relative">
        <svg width="50vw" height="100vh">
          {#each data as rider}
            <circle
              cx={xScale(rider.rank)}
              cy={yScale(rider.time)}
              r="20"
              fill={rider.color}
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
    background-color: purple;
  }

  .stage {
    position: absolute;
    bottom: 50px;
    left: 10px;
  }

  circle {
    transition:
      cx 500ms ease,
      cy 2000ms ease;
  }

  /* Scrollytelling CSS */
  .step {
    height: 120vh;
    width: 25vw;
    display: flex;
    place-items: center;
    justify-content: center;
    background-color: red;
    margin-left: auto;
    margin-right: 0;
  }

  .step1 {
    background-color: green;
  }

  .step2 {
    background-color: aqua;
  }

  /* .step-content {
    color: #ccc;
    border-radius: 5px;
    padding: 0.5rem 1rem;
    display: flex;
    flex-direction: column;
    justify-content: center;
    transition: background 500ms ease;
    box-shadow: 1px 1px 10px rgba(0, 0, 0, 0.2);
    z-index: 10;
  }*/

  /* .step.active {
    background-color: #5c5c5c00;
  } */
</style>
