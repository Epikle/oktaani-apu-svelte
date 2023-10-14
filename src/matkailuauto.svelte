<script>
  import Tulosta from './tulosta.svelte';
  let kokonaismassa, omamassa, pituus, matkustajapaikat;

  $: matkustajapaikat = Math.floor((kokonaismassa - omamassa - (pituus * 10 + 10)) / 85);
</script>

<div class="container">
  <h2>Matkailuauto</h2>
  <p class="lead">Matkailuauton matkustajamäärä</p>
  <div class="input-group input-group-sm mb-2">
    <div class="input-group-prepend">
      <span class="input-group-text">Kokonaismassa</span>
    </div>
    <input type="number" bind:value={kokonaismassa} class="form-control" placeholder="Kokonaismassa" />
    <div class="input-group-append">
      <span class="input-group-text">kg</span>
    </div>
  </div>
  <div class="input-group input-group-sm mb-1">
    <div class="input-group-prepend">
      <span class="input-group-text">Omamassa</span>
    </div>
    <input type="number" bind:value={omamassa} class="form-control" placeholder="Omamassa" />
    <div class="input-group-append">
      <span class="input-group-text">m</span>
    </div>
  </div>
  <small class="form-text text-muted mb-1"> Punnittu massa + kuljettaja 75 kg (käyttöönottoajankohdan mukaan). </small>
  <div class="input-group input-group-sm mb-1">
    <div class="input-group-prepend">
      <span class="input-group-text">Pituus</span>
    </div>
    <input type="number" bind:value={pituus} class="form-control" placeholder="Pituus" />
    <div class="input-group-append">
      <span class="input-group-text">m</span>
    </div>
  </div>
  <small class="form-text text-muted mb-1"> Matkailuauton kokonaispituus metreissä. </small>

  <div class="input-group input-group-sm mb-1 mt-4">
    <div class="input-group-prepend">
      <span class="input-group-text alert-success">Matkustajapaikat</span>
    </div>
    <input
      type="number"
      class="form-control"
      placeholder={kokonaismassa && omamassa && pituus ? matkustajapaikat : 'Täytä kaikki kentät'}
      disabled
    />
    <div class="input-group-append">
      <span class="input-group-text">matkustajaa</span>
    </div>
  </div>
  <small class="form-text text-muted mb-1">
    <strong>HUOM!</strong>
    Tässä vain matkustajapaikat, muista lisätä kuljettaja!
  </small>

  <Tulosta />
</div>

<style>
  .input-group-prepend span {
    width: 125px;
  }
</style>
