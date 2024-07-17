<script>
  export let width;
  export let height;
  export let curentStage;
  export let currentStep;
  export let initialStageData;
  import { scaleLinear } from "d3";

  $: mountainData = [
    { x: 0, y: 1, color: 0 },
    { x: 0.6, y: 0.92, color: 0.5 },
    { x: 0.3, y: 0.7, color: 0.8 },
    { x: 0.5, y: 0.6, color: 0.4 },
    { x: 0.2, y: 0.4, color: 0.2 },
    { x: 0.1, y: 0.3, color: 1 },
    { x: 0.6, y: 0.2, color: 0.4 },
    { x: 0, y: 0.1, color: 0.7 },
  ];

  $: xMountainScale = scaleLinear()
    .domain([0, 1])
    .range([-100, width / 4]);

  $: yMountainScale = scaleLinear()
    .domain([0, 1])
    .range([height * 1.4, 0]);

  $: colorMountainScale = scaleLinear()
    .domain([0, 1])
    .range(["#0B353E", "#43686F"]);

  let background = "#478692";
  $: initialStageData.map((e) => {
    if (e.id === curentStage + 1) {
      if (e.type === "flat") {
        background = "linear-gradient(#478692 85%, #9cd067)";
      } else if (e.type === "hilly") {
        background = "linear-gradient(#478692 85%, #609978)";
      } else {
        background = "#478692";
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
        {#if mountainData}
          {#each mountainData as mountain}<g
              transform="translate({xMountainScale(mountain.x)},{yMountainScale(
                mountain.y
              )}) scale(0.6)"
            >
              <path
                d="M107.913 32.0436C114.556 18.8114 133.444 18.8114 140.087 32.0436L248 247H0L107.913 32.0436Z"
                fill={colorMountainScale(mountain.color)}
              />
              <path
                fill-rule="evenodd"
                clip-rule="evenodd"
                d="M70.2186 107.129C73.6125 111.2 79.4718 115.502 90.5 119.5C114.161 128.077 121.726 120.384 127.788 114.22C131.974 109.964 135.443 106.436 143 109.5C149.229 112.025 154.664 116.251 160.298 120.631C169.222 127.569 178.645 134.895 192.509 136.466L140.087 32.0435C133.444 18.8114 114.556 18.8114 107.913 32.0436L70.2186 107.129Z"
                fill={mountain.color <= 0.2 ? "#F5F5F5" : "transparent"}
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
  }

  svg {
    width: 100%;
    height: 100%;
  }
</style>
