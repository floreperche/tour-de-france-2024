<script>
  export let width;
  export let height;
  export let curentStage;
  export let currentStep;
  export let initialStageData;
  import { scaleLinear } from "d3";

  $: hillData = [
    { x: 0, y: 0.98, color: 1, type: 1, size: 1 },
    { x: 0.4, y: 0.96, color: 3, type: 2, size: 1 },
    { x: 0.6, y: 0.96, color: 2, type: 1, size: 3 },
    { x: 0.5, y: 0.87, color: 1, type: 2, size: 2 },
    { x: 0.7, y: 0.86, color: 2, type: 2, size: 1 },
    { x: 0.6, y: 0.78, color: 3, type: 2, size: 1 },
    { x: 0.4, y: 0.75, color: 1, type: 2, size: 2 },
    { x: 0.3, y: 0.7, color: 3, type: 1, size: 2 },
    { x: 0.7, y: 0.64, color: 1, type: 2, size: 2 },
    { x: 0.5, y: 0.6, color: 2, type: 1, size: 3 },
    { x: 0.3, y: 0.52, color: 1, type: 2, size: 2 },
    { x: 0.7, y: 0.5, color: 3, type: 2, size: 1 },
    { x: 0.4, y: 0.46, color: 2, type: 2, size: 1 },
    { x: 0.2, y: 0.4, color: 1, type: 1, size: 1 },
    { x: 0.25, y: 0.36, color: 3, type: 2, size: 2 },
    { x: 0.6, y: 0.33, color: 1, type: 2, size: 1 },
    { x: 0.1, y: 0.3, color: 3, type: 1, size: 3 },
    { x: 0.6, y: 0.2, color: 2, type: 1, size: 2 },
    { x: 0.4, y: 0.13, color: 3, type: 2, size: 1 },
    { x: 0.4, y: 0.1, color: 1, type: 1, size: 1 },
    { x: 0.8, y: 0.05, color: 1, type: 2, size: 2 },
    { x: 0.6, y: 0.0, color: 2, type: 2, size: 2 },
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
      <line
        x1={width / 4 - 60}
        x2={width / 4 + 60}
        y1={50}
        y2={50}
        stroke="white"
        stroke-width="4"
        opacity="0.5"
      ></line>
      <text
        x={width / 4}
        y={100}
        fill="white"
        text-anchor="middle"
        opacity="0.5">STAGE {curentStage}</text
      >
    </svg>
  </div>
  <div class="landscape" style="background: {background}">
    {#if curentStage === currentStep + 1 || curentStage === currentStep || curentStage === currentStep + 2}
      <svg>
        <defs>
          <linearGradient id="dark-hill" x1="0%" x2="100%" y1="0%" y2="100%">
            <stop offset="0%" stop-color="#437D35 " />
            <stop offset="50%" stop-color="#235A16" />
          </linearGradient>
          <linearGradient id="medium-hill" x1="0%" x2="100%" y1="0%" y2="100%">
            <stop offset="0%" stop-color="#63A861 " />
            <stop offset="50%" stop-color="#1E7B1C" />
          </linearGradient>
          <linearGradient id="light-hill" x1="0%" x2="100%" y1="0%" y2="100%">
            <stop offset="0%" stop-color="#AABD83 " />
            <stop offset="50%" stop-color="#648D13" />
          </linearGradient>
        </defs>
        {#if hillData}
          {#each hillData as hill}<g
              transform="translate({xHillScale(hill.x)},{yHillScale(hill.y)})"
            >
              <!-- Hills with 3 sizes -->
              {#if hill.type === 1}{#if hill.size === 1}
                  <path
                    d="M197.778 60C197.778 26.8629 153.504 0 98.8889 0C44.2741 0 0 26.8629 0 60H197.778Z"
                    fill={hill.color === 1
                      ? "url(#dark-hill)"
                      : hill.color === 2
                        ? "url(#medium-hill)"
                        : "url(#light-hill)"}
                  />
                {:else if hill.size === 2}
                  <path
                    d="M240.917 101C240.917 45.2192 186.986 0 120.459 0C53.9312 0 0 45.2192 0 101H240.917Z"
                    fill={hill.color === 1
                      ? "url(#dark-hill)"
                      : hill.color === 2
                        ? "url(#medium-hill)"
                        : "url(#light-hill)"}
                  />
                {:else if hill.size === 3}
                  <path
                    d="M0 129H240.917C240.917 57.7553 186.986 0 120.459 0C53.9312 0 0 57.7553 0 129Z"
                    fill={hill.color === 1
                      ? "url(#dark-hill)"
                      : hill.color === 2
                        ? "url(#medium-hill)"
                        : "url(#light-hill)"}
                  />
                {/if}

                <!-- Bushes with two sizes -->
              {:else if hill.type === 2}
                {#if hill.size === 1}
                  <path
                    d="M89.0229 43H10.6972C-9.6071 33.7417 2.21916 14.6077 19.4399 22.0143C19.4399 22.0143 16.391 1.85168 32.1595 0C38.5914 0 52.0776 0 48.6947 20.1627C54.0599 8.84691 60.1634 9.14309 68.4056 12.5503C73.0824 14.4836 79.1946 22.0143 73.5926 30.8613C89.0229 20.1627 96.6229 37.445 89.0229 43Z"
                    fill={hill.color === 1
                      ? "url(#dark-hill)"
                      : hill.color === 2
                        ? "url(#medium-hill)"
                        : "url(#light-hill)"}
                  />
                {:else}
                  <path
                    d="M93.3601 39H1.428C-6.29833 16.6193 19.3441 7.09092 30.0938 16.5086C30.0938 16.5086 29.6358 7.34389e-05 55.1764 0C61.1111 -1.70645e-05 77.2356 4.76421 68.2775 23.5995C90.3367 9.41763 96.1221 30.7273 93.3601 39Z"
                    fill={hill.color === 1
                      ? "url(#dark-hill)"
                      : hill.color === 2
                        ? "url(#medium-hill)"
                        : "url(#light-hill)"}
                  />
                {/if}
              {/if}
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
    font-family: "Caveat Brush", cursive;
    font-size: 3em;
    letter-spacing: -2px;
  }

  svg {
    width: 100%;
    height: 100%;
  }

  path {
    -webkit-filter: drop-shadow(4px -4px 8px rgba(0, 0, 0, 0.3));
    filter: drop-shadow(4px -4px 8px rgba(0, 0, 0, 0.2));
  }
</style>
