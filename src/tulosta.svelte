<script>
  function tulosta() {
    window.print();
  }
</script>

<div class="row text-center my-5 d-print-none">
  <div class="col">
    <button type="button" class="btn btn-primary" on:click={tulosta}> Tulosta </button>
  </div>
</div>
<div class="row text-center mb-3 d-print-none">
  <div class="col">
    <small class="form-text text-muted mb-2 font-italic">
      Avustimet on tehty katsastajalle avuksi, käytät niitä omalla vastuulla, oktaaniAPU ei vastaa mahdollisista
      virheistä.
    </small>
    <small class="form-text text-muted mb-2">
      oktaani.com
      <strong>&copy;</strong>
      2020-2022
    </small>
  </div>
</div>

<style>
  .btn-primary {
    background-color: #c0002b;
    border-color: #c0002b;
  }
</style>
