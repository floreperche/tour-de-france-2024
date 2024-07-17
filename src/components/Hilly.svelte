<script>
  export let width;
  export let height;
  export let curentStage;
  export let currentStep;
  export let initialStageData;
  import { scaleLinear } from "d3";

  $: hillData = [
    { x: 0, y: 1, color: 0 },
    { x: 0.6, y: 0.92, color: 0.5 },
    { x: 0.3, y: 0.7, color: 0.8 },
    { x: 0.5, y: 0.6, color: 0.4 },
    { x: 0.2, y: 0.4, color: 0.2 },
    { x: 0.1, y: 0.3, color: 1 },
    { x: 0.6, y: 0.2, color: 0.4 },
    { x: 0, y: 0.1, color: 0.7 },
  ];

  $: xHillScale = scaleLinear()
    .domain([0, 1])
    .range([-100, width / 4]);

  $: yHillScale = scaleLinear()
    .domain([0, 1])
    .range([height * 1.4, 0]);

  $: colorHillScale = scaleLinear()
    .domain([0, 1])
    .range(["#235A16", "#648D13"]);

  let background = "#609978";
  $: initialStageData.map((e) => {
    if (e.id === curentStage + 1) {
      if (e.type === "flat") {
        background = "linear-gradient(#609978 85%, #9cd067)";
      } else if (e.type === "mountain") {
        background = "linear-gradient(#609978 85%, #478692)";
      } else {
        background = "#609978";
      }
    }
  });
</script>

<div class="step-content">
  <div class="step-count">
    <svg>
      <text
        x={width / 4}
        y={50}
        fill="white"
        text-anchor="middle"
        font-size="38"
        opacity="0.7">STAGE {curentStage}</text
      >
    </svg>
  </div>
  <div class="landscape" style="background: {background}">
    {#if curentStage === currentStep + 1 || curentStage === currentStep || curentStage === currentStep + 2}
      <svg>
        {#if hillData}
          {#each hillData as hill}<g
              transform="translate({xHillScale(hill.x)},{yHillScale(hill.y)})"
              ><path
                d="M0 86.5C0 38.7274 38.7274 0 86.5 0V0C134.273 0 173 38.7274 173 86.5V130H0V86.5Z"
                fill={colorHillScale(hill.color)}
              />
            </g>{/each}
        {/if}
      </svg>
    {/if}
  </div>
</div>

<style>
  .step-content {
    width: 100%;
    height: 100%;
    display: flex;
    place-items: center;
    justify-content: end;
  }

  .landscape {
    width: 25%;
    height: 100%;
  }
  .step-count {
    width: 50%;
    height: 100%;
    font-family: "Luckiest Guy", cursive;
    font-size: 38px;
  }

  svg {
    width: 100%;
    height: 100%;
  }
</style>
