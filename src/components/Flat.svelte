<script>
  export let width;
  export let height;
  export let curentStage;
  export let currentStep;
  export let initialStageData;
  import { scaleLinear } from "d3";
  $: grassData = Array.from({ length: 50 }).map(() => {
    return {
      x: Math.random(),
      y: Math.random(),
    };
  });

  $: xGrassScale = scaleLinear()
    .domain([0, 1])
    .range([0, width / 4]);

  $: yGrassScale = scaleLinear()
    .domain([0, 1])
    .range([height * 1.4, 0]);

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
    {#if curentStage === currentStep + 1 || curentStage === currentStep || curentStage === currentStep + 2}<svg
      >
        {#if grassData}
          {#each grassData as grass}<g
              transform="translate({xGrassScale(grass.x)},{yGrassScale(
                grass.y
              )})"
              ><path
                fill-rule="evenodd"
                clip-rule="evenodd"
                d="M15.3119 19.7397C15.4808 17.9882 15.5748 16.0453 15.5748 14C15.5748 6.26801 14.2316 0 12.5748 0C10.9179 0 9.57476 6.26801 9.57476 14C9.57476 15.4028 9.61897 16.7574 9.70125 18.0351C9.55136 17.7771 9.3975 17.5178 9.23978 17.2578C5.83756 11.6483 1.9311 7.79749 0.514444 8.65671C-0.902209 9.51593 0.707408 14.7598 4.10963 20.3693C7.51184 25.9787 11.4183 29.8296 12.835 28.9703C12.8739 28.9467 12.9105 28.9198 12.9449 28.8897C14.7136 28.613 17.7946 26.1846 20.6328 22.6764C24.1639 18.3119 25.9821 13.929 24.6941 12.8869C23.406 11.8448 19.4993 14.5381 15.9683 18.9026C15.7423 19.1818 15.5234 19.4612 15.3119 19.7397Z"
                fill="#7EA755"
              /></g
            >{/each}
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
