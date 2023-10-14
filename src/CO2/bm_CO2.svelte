<script>
  let omamassaCO2, tehoCO2, CO2, CO2R;

  $: if (omamassaCO2 && tehoCO2) {
    CO2 = (0.047 * omamassaCO2 + 0.561 * tehoCO2 + 56.621).toFixed(1);
    CO2R = Number(CO2).toFixed(0);
  }
</script>

<p class="mb-1">Bensiinimoottori ja manuaalivaihteisto</p>

<div class="input-group input-group-sm mb-2">
  <div class="input-group-prepend">
    <span class="input-group-text">Omamassa</span>
  </div>
  <input type="number" bind:value={omamassaCO2} class="form-control" placeholder="Omamassa" />
  <div class="input-group-append">
    <span class="input-group-text">kg</span>
  </div>
</div>

<div class="input-group input-group-sm mb-2">
  <div class="input-group-prepend">
    <span class="input-group-text">Teho</span>
  </div>
  <input type="number" bind:value={tehoCO2} class="form-control" placeholder="Teho" />
  <div class="input-group-append">
    <span class="input-group-text">kW</span>
  </div>
</div>

<div class="input-group input-group-sm mb-3">
  <div class="input-group-prepend">
    <span class="input-group-text alert-success">CO&#8322;</span>
  </div>
  <input
    type="text"
    class="form-control"
    placeholder={omamassaCO2 && tehoCO2
      ? '0,047 x ' + omamassaCO2 + ' + 0,561 x ' + tehoCO2 + ' + 56,621 = ' + CO2 + ' => ' + CO2R
      : '0,047 m + 0,561 p + 56,621'}
    disabled
  />
</div>

<style>
  .input-group-prepend span {
    width: 100px;
  }
</style>
