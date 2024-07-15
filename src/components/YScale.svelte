<script>
  export let currentStep;
  export let yScale;

  let yTicks = [0, 60, 120];
</script>

<svg
  width="25vw"
  height="100vh"
  class="scale"
  style="background-color : {currentStep + 1 === 9 ? '#E5E1D5' : '#615968'}"
>
  {#if currentStep >= 0}
    {#each yTicks as tick}
      {#if tick === 0}
        <text
          dominant-baseline="middle"
          fill="white"
          x="10"
          y={yScale(tick) - 8}
          >temps du
        </text>
        <text
          dominant-baseline="middle"
          fill="white"
          x="10"
          y={yScale(tick) + 8}>leader</text
        >
      {:else}
        <text
          dominant-baseline="middle"
          fill="white"
          x="10"
          y={yScale(tick) - 8}
          >{tick / 60} min
        </text>
        <text
          dominant-baseline="middle"
          fill="white"
          x="10"
          y={yScale(tick) + 8}>de retard</text
        >{/if}
    {/each}
  {/if}
</svg>

<style>
  .scale {
    transition: background-color 800ms ease;
  }
</style>
