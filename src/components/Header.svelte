<script>
  import HeaderLandscape from "./landscapes/HeaderLandscape.svelte";
</script>

<div class="header">
  <!-- Title -->
  <div class="title-container">
    <div></div>
    <div class="title">
      <div class="headline">
        <div><p>LE TOUR DE</p></div>
        <div><p>FRANCE '24</p></div>
      </div>

      <div>
        <svg width="203" height="6"
          ><path
            d="M168.594 1.34775L182.129 1.69717L193.764 1.797H196.851C200.017 2.5624 201.917 3.1614 202.55 3.59401C203.5 3.99334 202.946 4.40932 200.888 4.84193L198.751 5.39102C197.959 5.69052 196.693 5.84027 194.951 5.84027C194.16 5.97338 193.606 6.02329 193.289 5.99002C192.181 5.82363 183.158 5.49085 166.219 4.99168C166.219 4.99168 163.053 4.94176 156.721 4.84193C155.455 4.84193 151.576 4.77537 145.086 4.64226C138.754 4.54243 131.551 4.49251 123.477 4.49251L118.491 4.4426L112.079 4.19301C110.021 4.19301 108.834 4.20965 108.517 4.24293H104.718C101.235 4.17637 99.2567 4.12646 98.7818 4.09318H89.0461C81.7641 4.15973 75.8277 4.19301 71.2368 4.19301L56.5146 4.24293H45.5916L41.0799 4.34276H37.5181C34.6686 4.40932 32.4523 4.4426 30.8693 4.4426L19.2339 4.69218L12.8226 4.89185C10.4481 4.99168 8.0735 4.9584 5.69894 4.79201C3.16608 4.6589 1.50389 4.47587 0.712368 4.24293C-0.237456 4.00998 -0.237456 3.61065 0.712368 3.04492C1.50389 2.4792 2.45371 2.12978 3.56184 1.99667C4.51167 1.86356 4.90744 1.74709 4.74913 1.64725C6.01556 1.41431 7.5986 1.23128 9.49825 1.09817C10.1315 0.831947 11.2396 0.715474 12.8226 0.748752C14.4057 0.78203 15.8304 0.715474 17.0968 0.549085C18.205 0.382695 19.2339 0.299501 20.1838 0.299501C22.0834 0.299501 23.8248 0.266223 25.4078 0.199667L27.3074 0.249584C27.7824 0.14975 28.4947 0.0998334 29.4446 0.0998334L31.8191 0.0499169H35.1435C36.4099 0.0499169 37.2806 0.0332779 37.7555 0C38.2304 0 39.022 0.0332778 40.1301 0.0998334C40.2884 0.0998334 56.752 0.133111 89.521 0.199667L95.2199 0.249584H101.631C105.431 0.282862 110.1 0.299501 115.641 0.299501C127.989 0.499168 136.142 0.599002 140.099 0.599002C146.115 0.599002 155.613 0.848586 168.594 1.34775Z"
            fill="#ECB70C"
          />
        </svg>
      </div>
      <div><p class="subtitle">A scrollytelling visualisation</p></div>
    </div>
    <div class="header-landscape">
      <HeaderLandscape />
    </div>
  </div>

  <!-- Description -->
  <div class="description">
    <p>
      (Re)play the fight for the podium and see how Tadej Pogačar (UAD) won his
      third Tour de France. Stage by stage, he overtook his historical rival
      Jonas Vingegaard (TVL) and first-time participation Remco Evenepoel (SOQ).
    </p>

    <div class="scroll-indicator">
      <p>SCROLL <span>TO START THE RACE</span></p>
      <div>
        <svg width="22" height="23" viewBox="0 0 22 23">
          <path
            d="M21.6349 2.68148C22.1187 2.20179 22.122 1.42074 21.6423 0.93695C21.1626 0.453161 20.3816 0.449836 19.8978 0.929524L11.138 9.61503L2.45251 0.855262C1.97282 0.371473 1.19177 0.368149 0.707983 0.847836C0.224194 1.32752 0.220869 2.10858 0.700556 2.59236L10.2546 12.2281L11.1232 13.1041L11.9991 12.2355L21.6349 2.68148ZM21.2919 12.5444C21.7757 12.0647 21.7791 11.2837 21.2994 10.7999C20.8197 10.3161 20.0386 10.3128 19.5548 10.7924L10.7951 19.478L2.10956 10.7182C1.62987 10.2344 0.848817 10.2311 0.365028 10.7108C-0.118761 11.1904 -0.122086 11.9715 0.357602 12.4553L9.91166 22.091L10.7802 22.967L11.6562 22.0985L21.2919 12.5444Z"
            fill="#F5F5F5"
          />
        </svg>
      </div>
    </div>
  </div>
</div>

<style>
  .header {
    height: 100vh;
    width: 100%;
    background-color: #615968;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
  }

  .title-container {
    width: 100%;
    height: 50vh;
    background: linear-gradient(#cce0e3 92%, #615968 93%);
    display: flex;
    flex-direction: column;
    justify-content: space-between;
  }

  .header .title {
    padding-top: 4vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 4px;
    margin: 0 auto;
  }

  .header .title p {
    padding: 2px 6px;
    margin: 0 auto;
    font-family: "Caveat Brush", cursive;
    font-size: 50px;
    letter-spacing: 3.5px;
    text-align: justify;
    color: #50495f;
  }

  .header .title .subtitle {
    font-family: "Poppins", sans-serif;
    font-weight: 400;
    font-size: 14px;
    letter-spacing: 0px;
    text-transform: uppercase;
    padding-top: 8px;
  }

  .header-landscape {
    width: 100%;
    height: 150px;
  }

  .description {
    height: 45vh;
    padding: 0em 2em;
    color: white;
    font-size: 16px;
    font-weight: 200;
    letter-spacing: 0.5px;
    line-height: 1.4;
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    gap: 20px;
  }

  .description > p {
    text-align: justify;
    text-justify: inter-word;
    font-weight: 300;
  }

  .scroll-indicator {
    height: 15vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    gap: 10px;
  }

  .scroll-indicator p,
  .scroll-indicator span {
    font-family: "Caveat Brush", cursive;
    font-size: 20px;
    color: white;
  }

  @media (max-height: 576px) {
    .header .title p {
      font-size: 36px;
    }

    .description {
      flex-direction: row;
      align-items: center;
      font-size: 18px;
      padding: 1em;
    }

    .description > p {
      max-width: 60%;
      font-size: 14px;
    }

    .scroll-indicator {
      max-width: 40%;
      height: 100%;
      display: flex;
      align-items: center;
    }

    .scroll-indicator p,
    .scroll-indicator span {
      font-size: 16px;
      width: 100%;
      padding-top: 10px;
    }
    .scroll-indicator svg {
      width: 20;
      height: 20;
    }
  }
  @media (max-height: 400px) {
    .header .title .headline {
      display: flex;
    }
    .description {
      height: 20vh;
    }

    .description > p {
      font-size: 12px;
      max-width: 80%;
    }
    .scroll-indicator {
      max-width: 20%;
      flex-direction: row;
    }

    .scroll-indicator p {
      padding-top: 0px;
    }

    .scroll-indicator span {
      display: none;
    }
  }

  @media (min-height: 900px) {
    .header .title p {
      font-size: 70px;
    }

    .header .title .subtitle {
      font-size: 20px;
    }

    .description {
      padding: 4em;
    }

    .description > p {
      font-size: 18px;
    }
  }
</style>
