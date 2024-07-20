<script>
  export let width;
  export let height;
  export let curentStage;
  export let curentStep;
  export let initialStageData;
  import { scaleLinear } from "d3";

  $: hillData = [
    { x: 0, y: 0.98, color: 1, type: 1, size: 1 },
    { x: 0.4, y: 0.96, color: 3, type: 2, size: 1 },
    { x: 0.5, y: 0.87, color: 1, type: 2, size: 2 },
    { x: 0.6, y: 0.96, color: 2, type: 1, size: 3 },
    { x: 0.7, y: 0.86, color: 2, type: 2, size: 1 },
    { x: 0.6, y: 0.78, color: 3, type: 2, size: 1 },
    { x: 0.4, y: 0.75, color: 1, type: 2, size: 2 },
    { x: 0.3, y: 0.7, color: 3, type: 1, size: 2 },
    { x: 0.7, y: 0.64, color: 1, type: 2, size: 2 },
    { x: 0.3, y: 0.52, color: 1, type: 2, size: 2 },
    { x: 0.5, y: 0.6, color: 2, type: 1, size: 3 },
    { x: 0.7, y: 0.5, color: 3, type: 2, size: 1 },
    { x: 0.4, y: 0.44, color: 2, type: 2, size: 1 },
    { x: 0.2, y: 0.4, color: 1, type: 1, size: 1 },
    { x: 0.25, y: 0.36, color: 3, type: 2, size: 2 },
    { x: 0.6, y: 0.33, color: 1, type: 2, size: 1 },
    { x: 0.1, y: 0.3, color: 3, type: 1, size: 3 },
    { x: 0.4, y: 0.13, color: 3, type: 2, size: 1 },
    { x: 0.6, y: 0.2, color: 2, type: 1, size: 2 },
    { x: 0.4, y: 0.1, color: 1, type: 1, size: 1 },
    { x: 0.8, y: 0.05, color: 1, type: 2, size: 2 },
    { x: 0.6, y: 0.0, color: 2, type: 2, size: 2 },
  ];

  $: xHillScale = scaleLinear()
    .domain([0, 1])
    .range([-100, width / 4]);

  $: yHillScale = scaleLinear()
    .domain([0, 1])
    .range([height * 1.2, 0]);

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
    <svg style="height:100%">
      <g transform="translate({width / 4}, 0) scale({width / 320})">
        <line
          x1="-60"
          x2="60"
          y1={50}
          y2={50}
          stroke={curentStage === 9 ? "#615968" : "white"}
          stroke-width="4"
          opacity="0.5"
        ></line>
        <text
          x="0"
          y={100}
          fill={curentStage === 9 ? "#615968" : "white"}
          text-anchor="middle"
          font-size="38"
          opacity="0.5">STAGE {curentStage}</text
        ></g
      >
    </svg>
  </div>

  <div class="landscape" style="background: {background}">
    {#if curentStage === curentStep + 1 || curentStage === curentStep || curentStage === curentStep + 2}
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
        {#if !isNaN(xHillScale(1)) && !isNaN(yHillScale(1))}
          {#if hillData}
            {#each hillData as hill}<g
                transform="translate({xHillScale(hill.x) + 20},{yHillScale(
                  hill.y
                )}) scale({height / 720})"
              >
                <!-- Hills with 3 sizes -->
                {#if hill.type === 1}{#if hill.size === 1}
                    <path
                      d="M158.19 48.1793L0 48.1793C4.4172e-05 21.675 35.4122 0.188965 79.0952 0.188965C122.778 0.188965 158.19 21.675 158.19 48.1793Z"
                      fill={hill.color === 1
                        ? "url(#dark-hill)"
                        : hill.color === 2
                          ? "url(#medium-hill)"
                          : "url(#light-hill)"}
                    />
                  {:else if hill.size === 2}
                    <path
                      d="M193.049 81.1793C193.049 36.5636 149.913 0.395508 96.7014 0.395508C43.4901 0.395508 0.35376 36.5636 0.35376 81.1793H193.049Z"
                      fill={hill.color === 1
                        ? "url(#dark-hill)"
                        : hill.color === 2
                          ? "url(#medium-hill)"
                          : "url(#light-hill)"}
                    />
                  {:else if hill.size === 3}
                    <path
                      d="M0.304688 103.179H193C193 46.1949 149.864 0 96.6523 0C43.441 0 0.304688 46.1949 0.304688 103.179Z"
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
                      d="M49.9704 24.1368H6.00458C-5.39267 18.9399 1.24566 8.19958 10.912 12.3571C10.912 12.3571 9.20059 1.03939 18.0518 0C21.6622 0 29.2323 0 27.3333 11.3178C30.345 4.96595 33.771 5.13221 38.3975 7.04472C41.0226 8.12992 44.4536 12.3571 41.3091 17.3231C49.9704 11.3178 54.2365 21.0187 49.9704 24.1368Z"
                      fill={hill.color === 1
                        ? "url(#dark-hill)"
                        : hill.color === 2
                          ? "url(#medium-hill)"
                          : "url(#light-hill)"}
                    />
                  {:else}
                    <path
                      d="M52.6408 22.1366H1.0374C-3.29954 9.57387 11.0941 4.2254 17.1281 9.51171C17.1281 9.51171 16.871 0.245158 31.2075 0.245117C34.5388 0.245108 43.5898 2.91937 38.5614 13.492C50.9437 5.53143 54.1912 17.493 52.6408 22.1366Z"
                      fill={hill.color === 1
                        ? "url(#dark-hill)"
                        : hill.color === 2
                          ? "url(#medium-hill)"
                          : "url(#light-hill)"}
                    />
                  {/if}
                {/if}
              </g>{/each}
          {/if}{/if}
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
