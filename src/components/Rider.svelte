<script>
  export let rider;

  // $: console.log(xScale(rider.rank));
</script>

<circle cx={rider.x} cy={rider.y} r="10" fill={rider.color}></circle>
