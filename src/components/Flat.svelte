<script>
  export let width;
  export let height;
  export let curentStage;
  export let curentStep;
  export let initialStageData;
  import { scaleLinear } from "d3";

  $: grassData = [
    // Grass
    { x: 0.4, y: 0.96, color: 3, type: 2, size: 1 },
    { x: 0.5, y: 0.87, color: 1, type: 2, size: 1 },
    { x: 0.7, y: 0.86, color: 2, type: 2, size: 1 },
    { x: 0.6, y: 0.78, color: 3, type: 2, size: 1 },
    { x: 0.4, y: 0.75, color: 1, type: 2, size: 1 },
    { x: 0.7, y: 0.64, color: 1, type: 2, size: 1 },
    { x: 0.3, y: 0.52, color: 1, type: 2, size: 1 },
    { x: 0.4, y: 0.5, color: 3, type: 2, size: 1 },
    { x: 0.2, y: 0.49, color: 2, type: 2, size: 1 },
    { x: 0.25, y: 0.36, color: 3, type: 2, size: 1 },
    { x: 0.6, y: 0.26, color: 1, type: 2, size: 1 },
    { x: 0.2, y: 0.15, color: 2, type: 2, size: 1 },
    { x: 0.4, y: 0.13, color: 3, type: 2, size: 1 },
    { x: 0.3, y: 0.04, color: 1, type: 2, size: 1 },
    { x: 0.2, y: 0.02, color: 2, type: 2, size: 1 },
    // Bushes
    { x: 0.2, y: 0.93, color: 2, type: 3, size: 1 },
    { x: 0.1, y: 0.87, color: 1, type: 3, size: 1 },
    { x: 0.7, y: 0.82, color: 3, type: 3, size: 2 },
    { x: 0.15, y: 0.79, color: 3, type: 3, size: 1 },
    { x: 0.4, y: 0.75, color: 2, type: 3, size: 2 },
    { x: 0.7, y: 0.64, color: 1, type: 3, size: 2 },
    { x: 0.2, y: 0.54, color: 3, type: 3, size: 1 },
    { x: 0.7, y: 0.5, color: 1, type: 3, size: 2 },
    { x: 0.4, y: 0.44, color: 2, type: 3, size: 1 },
    { x: 0.65, y: 0.36, color: 2, type: 3, size: 1 },
    { x: 0.6, y: 0.33, color: 3, type: 3, size: 2 },
    { x: 0.3, y: 0.17, color: 1, type: 3, size: 1 },
    { x: 0.8, y: 0.05, color: 2, type: 3, size: 2 },
    { x: 0.6, y: 0.0, color: 1, type: 3, size: 1 },
    // Tree
    { x: 0, y: 0.98, color: 1, type: 1, size: 1 },
    { x: 0.6, y: 0.96, color: 2, type: 1, size: 1 },
    { x: 0.4, y: 0.94, color: 3, type: 1, size: 1 },
    { x: 0.3, y: 0.8, color: 1, type: 1, size: 1 },
    { x: 0.7, y: 0.79, color: 2, type: 1, size: 1 },
    { x: 0.3, y: 0.7, color: 3, type: 1, size: 1 },
    { x: 0.5, y: 0.6, color: 2, type: 1, size: 1 },
    { x: 0.2, y: 0.4, color: 1, type: 1, size: 1 },
    { x: 0.1, y: 0.3, color: 3, type: 1, size: 1 },
    { x: 0.6, y: 0.2, color: 2, type: 1, size: 1 },
    { x: 0.4, y: 0.1, color: 1, type: 1, size: 1 },
  ];

  $: xGrassScale = scaleLinear()
    .domain([0, 1])
    .range([-20, width / 4]);

  $: yGrassScale = scaleLinear()
    .domain([0, 1])
    .range([height * 1.2, 0]);

  let background = "#9cd067";
  $: initialStageData.map((e) => {
    if (e.id === curentStage + 1) {
      if (e.type === "hilly") {
        background = "linear-gradient(#9cd067 85%, #609978)";
      } else if (e.type === "mountain") {
        background = "linear-gradient(#9cd067 85%, #478692)";
      } else {
        background = "#9cd067";
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
        font-size="38"
        opacity="0.5">STAGE {curentStage}</text
      >
    </svg>
  </div>

  <div class="landscape" style="background: {background}">
    {#if curentStage === curentStep + 1 || curentStage === curentStep || curentStage === curentStep + 2}
      <svg width={width / 4} height="100%">
        <defs>
          <linearGradient id="stem" x1="0%" x2="100%" y1="0%" y2="100%">
            <stop offset="0%" stop-color="#935A48 " />
            <stop offset="50%" stop-color="#6D5249" />
          </linearGradient>
          <linearGradient id="dark" x1="0%" x2="100%" y1="0%" y2="100%">
            <stop offset="0%" stop-color="#82A75D " />
            <stop offset="50%" stop-color="#577A34" />
          </linearGradient>
          <linearGradient id="medium" x1="0%" x2="100%" y1="0%" y2="100%">
            <stop offset="0%" stop-color="#90B56B " />
            <stop offset="50%" stop-color="#6A9044" />
          </linearGradient>
          <linearGradient id="light" x1="0%" x2="100%" y1="0%" y2="100%">
            <stop offset="0%" stop-color="#9EC17B " />
            <stop offset="50%" stop-color="#7EA755" />
          </linearGradient>
        </defs>
        {#if !isNaN(xGrassScale(1)) && !isNaN(yGrassScale(1))}
          {#if grassData}
            {#each grassData as grass}<g
                transform="translate({xGrassScale(grass.x)},{yGrassScale(
                  grass.y
                )})"
              >
                <!-- Trees -->
                {#if grass.type === 1}<rect
                    x="22.083"
                    y="55.9783"
                    width="5.25792"
                    height="31.0217"
                    fill="url(#stem)"
                  />
                  <path
                    d="M1.63664 57.0299C-2.56969 66.757 15.9486 66.4363 24.624 66.4363C35.2879 66.4363 44.7522 63.0132 44.2264 58.8068C43.7006 54.6004 36.0766 57.2871 44.2264 45.1996C52.3761 33.1121 49.4843 30.7458 41.0716 24.6937C38.2557 22.6679 54.2164 8.33147 36.3395 7.27961C30.774 6.95214 33.7105 -1.13304 24.624 0.449466C12.3522 2.58673 17.7884 8.39416 9.11302 9.44574C0.437631 10.4973 2.27755 19.6987 6.484 23.3792C10.6904 27.0598 -4.93564 35.2095 1.63664 39.9417C8.20892 44.6738 5.84298 47.3027 1.63664 57.0299Z"
                    fill={grass.color === 1
                      ? "url(#dark)"
                      : grass.color === 2
                        ? "url(#medium)"
                        : "url(#light)"}
                  />
                  <!-- Grass elements -->
                {:else if grass.type === 2}<path
                    d="M18.5378 28.0068C18.632 27.0301 18.6844 25.9468 18.6844 24.8063C18.6844 20.495 17.9355 17 17.0116 17C16.0878 17 15.3389 20.495 15.3389 24.8063C15.3389 25.5885 15.3635 26.3438 15.4094 27.0563C15.3258 26.9124 15.24 26.7678 15.152 26.6227C13.255 23.495 11.0768 21.3478 10.2868 21.8269C9.49694 22.306 10.3944 25.2299 12.2915 28.3577C14.1885 31.4855 16.3667 33.6327 17.1567 33.1536C17.1783 33.1404 17.1988 33.1254 17.2179 33.1086C18.2041 32.9545 19.9221 31.6004 21.5048 29.6441C23.4737 27.2106 24.4875 24.7667 23.7693 24.1856C23.0511 23.6046 20.8727 25.1063 18.9039 27.5399C18.7779 27.6956 18.6558 27.8514 18.5378 28.0068Z"
                    fill={grass.color === 1
                      ? "url(#dark)"
                      : grass.color === 2
                        ? "url(#medium)"
                        : "url(#light)"}
                  />
                  <!-- Bushes (two types) -->
                {:else if grass.type === 3}
                  {#if grass.size === 1}
                    <path
                      d="M49.9704 24.1368H6.00458C-5.39267 18.9399 1.24566 8.19958 10.912 12.3571C10.912 12.3571 9.20059 1.03939 18.0518 0C21.6622 0 29.2323 0 27.3333 11.3178C30.345 4.96595 33.771 5.13221 38.3975 7.04472C41.0226 8.12992 44.4536 12.3571 41.3091 17.3231C49.9704 11.3178 54.2365 21.0187 49.9704 24.1368Z"
                      fill={grass.color === 1
                        ? "url(#dark)"
                        : grass.color === 2
                          ? "url(#medium)"
                          : "url(#light)"}
                    />
                  {:else if grass.size === 2}<path
                      d="M52.6408 22.1366H1.0374C-3.29954 9.57387 11.0941 4.2254 17.1281 9.51171C17.1281 9.51171 16.871 0.245158 31.2075 0.245117C34.5388 0.245108 43.5898 2.91937 38.5614 13.492C50.9437 5.53143 54.1912 17.493 52.6408 22.1366Z"
                      fill={grass.color === 1
                        ? "url(#dark)"
                        : grass.color === 2
                          ? "url(#medium)"
                          : "url(#light)"}
                    />
                  {/if}
                {/if}
              </g>{/each}
          {/if}
        {/if}
      </svg>{/if}
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

  .step-count {
    width: 50vh;
  }

  .step-count svg {
    width: 100%;
    max-width: 50vw;
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

  .landscape svg {
    width: 100%;
    height: 100%;
  }

  path {
    -webkit-filter: drop-shadow(3px -3px 4px rgba(0, 0, 0, 0.2));
    filter: drop-shadow(3px -3px 4px rgba(0, 0, 0, 0.2));
  }
</style>
