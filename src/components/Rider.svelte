<script>
  export let rider;
  export let xScale;
  export let yScale;
  export let curentStep;
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

<g transform="translate({$tX - 13},{$tY - 90}) ">
  <path
    fill-rule="evenodd"
    clip-rule="evenodd"
    d="M14.3258 0C13.9708 0 13.683 0.282798 13.683 0.637839V16.7143H13.2544C12.781 16.7143 12.3973 17.098 12.3973 17.5714V30.8571V31.2857H12.8258H15.8258H16.2544V30.8571V17.5714C16.2544 17.098 15.8707 16.7143 15.3973 16.7143H14.9687V0.637839C14.9687 0.282799 14.6809 0 14.3258 0ZM13.683 17.1429V28.545C13.683 29.9136 14.9687 29.9136 14.9687 28.545V17.1429H15.3973C15.634 17.1429 15.8258 17.3347 15.8258 17.5714V30.8571H12.8258V17.5714C12.8258 17.3347 13.0177 17.1429 13.2544 17.1429H13.683Z"
    fill="#FBFDF6"
  />
  <path
    fill-rule="evenodd"
    clip-rule="evenodd"
    d="M13.6829 64.7144H14.9687V79.7144H15.3972H15.8258H25.0662C25.1405 79.2063 25.2576 78.8045 25.4478 78.56C25.7104 78.2973 26.7609 78.4286 26.4983 78.9539C26.0974 79.8703 26.1461 81.2863 26.1978 82.7879C26.2645 84.7291 26.3363 86.8134 25.4477 88.1462C25.0538 88.5401 24.5285 88.0148 24.3972 87.3583C24.8529 85.9913 24.8891 84.108 24.9217 82.4122C24.9342 81.7571 24.9463 81.13 24.9818 80.5715H15.8258V82.2858C15.8258 82.7592 15.442 83.1429 14.9687 83.1429L14.9687 94.9141C14.9687 96.3621 13.6829 96.3621 13.6829 94.9141V83.1429C13.2096 83.1429 12.8258 82.7592 12.8258 82.2858V80.5715H3.66983C3.70531 81.13 3.71736 81.7571 3.72994 82.4122C3.76252 84.108 3.7987 85.9913 4.25437 87.3583C4.12305 88.0148 3.59781 88.5401 3.20386 88.1462C2.31534 86.8134 2.38705 84.7291 2.45384 82.7879C2.50551 81.2863 2.55423 79.8703 2.15331 78.9539C1.89068 78.4286 2.94119 78.2973 3.20383 78.56C3.39399 78.8045 3.51109 79.2063 3.58536 79.7144H12.8258H13.2544H13.6829V64.7144ZM13.2544 80.5715V82.2858C13.2544 82.5225 13.4462 82.7144 13.6829 82.7144V80.5715H13.2544ZM14.9687 80.5715L14.9687 82.7144C15.2053 82.7144 15.3972 82.5225 15.3972 82.2858V80.5715H14.9687Z"
    fill="#FBFDF6"
  />
  <path
    d="M2.11146 60.8569H6.82575C6.82575 60.8569 6.18285 67.2855 6.18289 69.6426C6.18294 71.9998 7.25432 76.4998 6.82575 78.2141C6.39718 79.9284 8.54004 80.1426 6.82575 81.6426C5.11146 83.1426 4.46865 82.2855 4.04008 80.7855C3.61151 79.2855 4.52341 79.7261 4.46865 77.7855C4.36932 74.2653 2.44132 69.1495 2.11147 65.7855C1.8652 63.2738 2.11146 60.8569 2.11146 60.8569Z"
    fill="#CF8F7B"
  />
  <path
    d="M26.7867 60.8569H22.0724C22.0724 60.8569 22.7153 67.2855 22.7153 69.6426C22.7153 71.9998 21.6439 76.4998 22.0724 78.2141C22.501 79.9284 20.3582 80.1426 22.0724 81.6426C23.7867 83.1426 24.4295 82.2855 24.8581 80.7855C25.2867 79.2855 24.3748 79.7261 24.4295 77.7855C24.5289 74.2653 26.4569 69.1495 26.7867 65.7855C27.033 63.2738 26.7867 60.8569 26.7867 60.8569Z"
    fill="#CF8F7B"
  />
  <g filter="url(#filter0_d_55_773)">
    <path
      fill-rule="evenodd"
      clip-rule="evenodd"
      d="M14.4286 28.3263C11.4262 28.1113 8.55019 29.3443 6.92857 31.7227C4.75697 34.9078 4.81115 37.6037 4.8927 41.6609C4.93185 43.6089 4.97732 45.8707 4.78574 48.6512C4.34569 55.038 2 61.0799 2 61.0799H6.81601C7.41582 56.7045 10.5958 53.3658 14.4286 53.3658L14.4286 28.3263ZM14.4286 28.3265C17.4309 28.1115 20.307 29.3445 21.9286 31.7229C24.1002 34.908 24.046 37.6039 23.9644 41.6611C23.9253 43.6091 23.8798 45.8709 24.0714 48.6515C24.5115 55.0382 26.8571 61.0801 26.8571 61.0801H22.0411C21.4413 56.7047 18.2614 53.366 14.4286 53.366V28.3265Z"
      fill={rider.rank === 1 ? "#ECB70C" : rider.color}
    />
  </g>
  <g filter="url(#filter1_d_55_773)">
    <path
      fill-rule="evenodd"
      clip-rule="evenodd"
      d="M6.92861 31.7227C8.55022 29.3443 11.4263 28.1113 14.4286 28.3263V36.8744C14.3572 36.8739 14.2858 36.8737 14.2143 36.8737C10.8937 36.8737 7.73789 37.3685 4.88885 38.2586C4.98732 35.904 5.42304 33.9309 6.92861 31.7227ZM23.9738 38.398C23.8866 35.9816 23.4638 33.9745 21.9286 31.7229C20.307 29.3446 17.431 28.1115 14.4286 28.3265V36.8744C17.84 36.8963 21.0733 37.4403 23.9738 38.398Z"
      fill="black"
    />
  </g>
  <g filter="url(#filter2_d_55_773)">
    <path
      d="M12.3973 52.2857C13.7857 52.0714 14.4286 52.0714 16.3468 52.2858C18.0702 52.4784 18.7746 56.3442 19.0605 59.7275C19.2974 62.531 16.9926 64.7932 14.1792 64.7932V64.7932C11.4948 64.7932 9.2443 62.7263 9.35967 60.0445C9.50556 56.6534 10.1566 52.6316 12.3973 52.2857Z"
      fill={rider.color}
    />
  </g>
  <defs>
    <filter
      id="filter0_d_55_773"
      x="0.885714"
      y="27.6165"
      width="27.0857"
      height="35.0064"
      filterUnits="userSpaceOnUse"
      color-interpolation-filters="sRGB"
    >
      <feFlood flood-opacity="0" result="BackgroundImageFix" />
      <feColorMatrix
        in="SourceAlpha"
        type="matrix"
        values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 127 0"
        result="hardAlpha"
      />
      <feOffset dy="0.428571" />
      <feGaussianBlur stdDeviation="0.557143" />
      <feComposite in2="hardAlpha" operator="out" />
      <feColorMatrix
        type="matrix"
        values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0.25 0"
      />
      <feBlend
        mode="normal"
        in2="BackgroundImageFix"
        result="effect1_dropShadow_55_773"
      />
      <feBlend
        mode="normal"
        in="SourceGraphic"
        in2="effect1_dropShadow_55_773"
        result="shape"
      />
    </filter>
    <filter
      id="filter1_d_55_773"
      x="1.76028"
      y="26.888"
      width="25.342"
      height="16.3528"
      filterUnits="userSpaceOnUse"
      color-interpolation-filters="sRGB"
    >
      <feFlood flood-opacity="0" result="BackgroundImageFix" />
      <feColorMatrix
        in="SourceAlpha"
        type="matrix"
        values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 127 0"
        result="hardAlpha"
      />
      <feOffset dy="1.71429" />
      <feGaussianBlur stdDeviation="1.56429" />
      <feComposite in2="hardAlpha" operator="out" />
      <feColorMatrix
        type="matrix"
        values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0.25 0"
      />
      <feBlend
        mode="normal"
        in2="BackgroundImageFix"
        result="effect1_dropShadow_55_773"
      />
      <feBlend
        mode="normal"
        in="SourceGraphic"
        in2="effect1_dropShadow_55_773"
        result="shape"
      />
    </filter>
    <filter
      id="filter2_d_55_773"
      x="8.06969"
      y="49.5536"
      width="13.1504"
      height="16.097"
      filterUnits="userSpaceOnUse"
      color-interpolation-filters="sRGB"
    >
      <feFlood flood-opacity="0" result="BackgroundImageFix" />
      <feColorMatrix
        in="SourceAlpha"
        type="matrix"
        values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 127 0"
        result="hardAlpha"
      />
      <feOffset dx="0.428571" dy="-0.857143" />
      <feGaussianBlur stdDeviation="0.857143" />
      <feComposite in2="hardAlpha" operator="out" />
      <feColorMatrix
        type="matrix"
        values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0.25 0"
      />
      <feBlend
        mode="normal"
        in2="BackgroundImageFix"
        result="effect1_dropShadow_55_773"
      />
      <feBlend
        mode="normal"
        in="SourceGraphic"
        in2="effect1_dropShadow_55_773"
        result="shape"
      />
    </filter>
  </defs>
</g>
{#if curentStep >= 0 && rider.rank <= 3}
  <text
    dominant-baseline="middle"
    fill="white"
    x="20"
    y="0"
    transform="translate({$tX},{$tY - 90}) rotate(-90)"
  >
    {rider.name}</text
  >=
{/if}

<style>
  g {
    -webkit-filter: drop-shadow(3px -3px 4px rgba(0, 0, 0, 0.2));
    filter: drop-shadow(3px -3px 4px rgba(0, 0, 0, 0.2));
  }
</style>
