<script>
  import logo from "../assets/visuals/logo_light2_png.png";
</script>

<div class="footer">
  <div>
    <p>A project designed and developed by</p>
    <div>
      <a href="https://www.wildvariables.com" target="_blank"
        ><img src={logo} alt="logo Wild Variables" /></a
      >
    </div>
    <p>
      You can contact me <a
        href="https://twitter.com/wildvariables"
        target="_blank">here</a
      >
    </p>
  </div>
  <p>
    Source: <a href="https://www.letour.fr/fr/" target="_blank">www.letour.fr</a
    >
    •
    <a
      href="https://github.com/wildvariables/tour-de-france-2024"
      target="_blank">See the code</a
    >
  </p>
</div>

<style>
  .footer {
    color: white;
    background-color: #504c53;
    padding: 40px 20px;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 20px;
    text-align: center;
  }

  .footer div {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 10px;
  }

  .footer a {
    color: white;
    text-align: center;
    display: inline-table;
    position: relative;
  }

  .footer img {
    width: 100px;
  }
</style>
