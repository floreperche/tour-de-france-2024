<script>
  import { scaleLinear } from "d3";
  let width;
</script>

<div bind:clientWidth={width} class="container">
  <div
    style="width: {width / 4}px; background-color: #5C5C6C; "
    class="scale"
  ></div>
  <div
    style="width: {width / 2}px; background-color: #5C5C5C;"
    class="viz"
  ></div>
  <div
    style="width: {width / 4}px; background-color: #7EA755; "
    class="background"
  ></div>
</div>

<style>
  .container {
    display: flex;
  }

  .container div {
    height: 100vh;
  }
</style>
