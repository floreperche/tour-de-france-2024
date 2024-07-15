<script>
  export let rider;
  export let xScale;
  export let yScale;

  $: console.log(xScale(rider.rank));
</script>

<g
  class="rider"
  transform="translate({xScale(rider.rank)},{yScale(rider.time)} )"
>
  <circle cx="0" cy="0" r="10" fill={rider.color}></circle>
</g>

<style>
  .rider {
    transition: transform 0.3s;
  }
</style>
