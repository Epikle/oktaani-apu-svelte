<script>
  let omamassaCO2, CO2, CO2R;

  $: if (omamassaCO2) {
    CO2 = (0.116 * omamassaCO2 - 57.147).toFixed(1);
    CO2R = Number(CO2).toFixed(0);
  }
</script>

<style>
  .input-group-prepend span {
    width: 100px;
  }
</style>

<p class="mb-1">Bensiinimoottori ja sähköhybridi</p>

<div class="input-group input-group-sm mb-2">
  <div class="input-group-prepend">
    <span class="input-group-text">Omamassa</span>
  </div>
  <input
    type="number"
    bind:value={omamassaCO2}
    class="form-control"
    placeholder="Omamassa" />
  <div class="input-group-append">
    <span class="input-group-text">kg</span>
  </div>
</div>

<div class="input-group input-group-sm mb-3">
  <div class="input-group-prepend">
    <span class="input-group-text alert-success">CO&#8322;</span>
  </div>
  <input
    type="text"
    class="form-control"
    placeholder={omamassaCO2 ? '0,116 x ' + omamassaCO2 + ' - 57,147 = ' + CO2 + ' => ' + CO2R : '0,116m - 57,147'}
    disabled />

</div>
