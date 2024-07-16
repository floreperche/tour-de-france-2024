<script>
  export let rider;
  export let xScale;
  export let yScale;
  export let currentStep;
  import { tweened } from "svelte/motion";
  import { cubicInOut } from "svelte/easing";

  const tX = tweened(undefined, {
    delay: 0,
    duration: 1000,
    easing: cubicInOut,
  });

  const tY = tweened(undefined, {
    duration: 2000,
    easing: cubicInOut,
  });

  $: tX.set(xScale(rider.rank));
  $: tY.set(yScale(rider.time));
</script>

<!-- <circle cx={rider.x} cy= r="10" fill={rider.color}></circle> -->

<g transform="translate({$tX - 13},{$tY - 110}) ">
  <ellipse cx="12.7086" cy="100.055" rx="12.7086" ry="1.21034" fill="#121313" />
  <ellipse cx="12.9103" cy="100.257" rx="1.21034" ry="16.7431" fill="#121313" />
  <ellipse cx="12.9103" cy="100.257" rx="2.01724" ry="6.6569" fill="#121313" />
  <ellipse cx="12.9103" cy="16.7431" rx="1.21034" ry="16.7431" fill="#121313" />
  <ellipse cx="12.9103" cy="16.7431" rx="2.01724" ry="6.6569" fill="#121313" />
  <ellipse cx="20.9793" cy="75.0414" rx="1.21034" ry="26.6276" fill="#BC7863" />
  <ellipse cx="4.84133" cy="75.0414" rx="1.21034" ry="26.6276" fill="#BC7863" />
  <ellipse
    cx="12.9103"
    cy="55.0707"
    rx="10.0862"
    ry="20.7776"
    fill={rider.rank === 1 ? "yellow" : rider.color}
  />
  <circle cx="12.9104" cy="76.2517" r="5.64828" fill="#121313" />
</g>
{#if currentStep >= 0 && rider.rank <= 3}
  <text
    dominant-baseline="middle"
    fill="white"
    x="20"
    y="0"
    transform="translate({$tX},{$tY - 100}) rotate(-90)"
  >
    {rider.name}</text
  >=
{/if}
