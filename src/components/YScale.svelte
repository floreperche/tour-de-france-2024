<script>
  export let curentStep;
  export let maxYScale;
  export let height;
  export let heightMargin;
  import { tweened } from "svelte/motion";
  import { cubicInOut } from "svelte/easing";
  import { scaleLinear } from "d3";

  // Scales
  $: yScale = scaleLinear()
    .domain([0, $tYScale])
    .range([height - heightMargin, 10]);

  const tYScale = tweened(undefined, {
    duration: 2000,
    easing: cubicInOut,
  });

  let scaleWidth;

  // Manage dynamic scale
  $: {
    if (curentStep === undefined) {
      tYScale.set(0);
    } else {
      tYScale.set(maxYScale);
    }
  }

  $: yTicks = [0, 60, 120, 240, 360];

  $: {
    if (maxYScale === 130) {
      yTicks = [0, 60, 120, 240, 360, 480, 600];
    } else if (maxYScale === 500) {
      yTicks = [0, 120, 240, 360, 480, 600];
    } else {
      yTicks = [0, 120, 240, 360, 480, 600];
    }
  }
</script>

<div bind:clientWidth={scaleWidth} class="scale-container">
  <svg width={scaleWidth} height="100vh" class="scale">
    {#if curentStep >= 0}
      {#each yTicks as tick}
        {#if tick === 0}
          <text
            dominant-baseline="middle"
            text-anchor="end"
            fill={curentStep + 1 === 9 ? "#615968" : "white"}
            x={scaleWidth - 20}
            y={yScale(tick) - 8}
            >Leader
          </text>
          <text
            dominant-baseline="middle"
            text-anchor="end"
            fill={curentStep + 1 === 9 ? "#615968" : "white"}
            x={scaleWidth - 20}
            y={yScale(tick) + 8}>time</text
          >
        {:else}
          <text
            text-anchor="end"
            dominant-baseline="middle"
            fill={curentStep + 1 === 9 ? "#615968" : "white"}
            x={scaleWidth - 20}
            y={yScale(tick)}
            >+ {tick / 60}min
          </text>
        {/if}
        <rect
          x={scaleWidth - 7}
          y={yScale(tick) - 8}
          width="5"
          height="20"
          fill={curentStep + 1 === 9 ? "#615968" : "white"}
          opacity="0.5"
        />
        <rect
          x={scaleWidth - 5}
          y={yScale(tick) - 12}
          width="5"
          height="20"
          fill={curentStep + 1 === 9 ? "#615968" : "white"}
          opacity="0.5"
        />
      {/each}
    {/if}
  </svg>
</div>

<style>
  .scale-container {
    width: 25%;
  }
</style>
