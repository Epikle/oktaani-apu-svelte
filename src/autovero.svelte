<script>
  import Tulosta from "./tulosta.svelte";

  let kokonaismassa, omamassa, teho, kantavuus, osamaara;
  let tulos = false;

  $: kantavuus = kokonaismassa - omamassa;
  $: osamaara = (teho / kokonaismassa).toFixed(2);

  $: if (
    kantavuus >= 680 &&
    kantavuus < 1000 &&
    osamaara <= 0.05 &&
    kokonaismassa > 2500
  ) {
    tulos = true;
  } else if (kantavuus >= 1000 && osamaara <= 0.06 && kokonaismassa > 2500) {
    tulos = true;
  } else {
    tulos = false;
  }
</script>

<style>
  .input-group-prepend span {
    width: 115px;
  }
</style>

<div class="container">

  <h2>Autoverolaki 8 §</h2>
  <p class="lead">
    Tarkista täyttääkö pakettiauto autoverolain 8 § edellytykset
  </p>

  <div class="input-group input-group-sm mb-2">
    <div class="input-group-prepend">
      <span class="input-group-text">Kokonaismassa</span>
    </div>
    <input
      type="number"
      bind:value={kokonaismassa}
      class="form-control"
      placeholder="Kokonaismassa" />
    <div class="input-group-append">
      <span class="input-group-text">kg</span>
    </div>
  </div>
  <div class="input-group input-group-sm mb-2">
    <div class="input-group-prepend">
      <span class="input-group-text">Omamassa</span>
    </div>
    <input
      type="number"
      bind:value={omamassa}
      class="form-control"
      placeholder="Omamassa" />
    <div class="input-group-append">
      <span class="input-group-text">kg</span>
    </div>
  </div>
  <div class="input-group input-group-sm mb-2">
    <div class="input-group-prepend">
      <span class="input-group-text">Teho</span>
    </div>
    <input
      type="number"
      bind:value={teho}
      class="form-control"
      placeholder="Teho" />
    <div class="input-group-append">
      <span class="input-group-text">kW</span>
    </div>
  </div>

  <p class="mb-2">Tulos</p>
  <div class="input-group input-group-sm mb-2">
    <div class="input-group-prepend">
      <span class="input-group-text">Kantavuus</span>
    </div>
    <input
      type="number"
      value={kantavuus}
      class="form-control"
      placeholder="Kantavuus"
      disabled />
    <div class="input-group-append">
      <span class="input-group-text">kg</span>
    </div>
  </div>
  <div class="input-group input-group-sm mb-2">
    <div class="input-group-prepend">
      <span class="input-group-text">Osamäärä</span>
    </div>
    <input
      type="number"
      value={osamaara}
      class="form-control"
      placeholder="Osamäärä"
      disabled />
  </div>
  <div class="input-group input-group-sm mb-2">
    <div class="input-group-prepend">
      <span class="input-group-text alert-success">Onnistuuko</span>
    </div>
    <input
      type="text"
      class="form-control"
      placeholder={kokonaismassa && omamassa && teho ? [tulos ? 'Onnistuu' : 'Ei onnistu'] : 'Täytä kaikki kentät'}
      disabled />
  </div>

  <p class="font-italic small text-muted mb-0">
    Pakettiauto on alennetun autoveron alainen, jos se täyttää seuraavat
    edellytykset (autoverolaki 8§):
  </p>
  <p class="font-italic small text-muted mb-0">
    - auton kokonaismassa on yli 2 500 kg
  </p>
  <p class="font-italic small text-muted mb-0">
    - autossa ei ole muita istuimia tai istuinten kiinnitykseen tarkoitettuja
    laitteita (pl. pyörätuolin kiinnittämiseen tarkoitetut laitteet) kuin
    kuljettajan istuin ja tämän vieressä olevat istuimet
  </p>
  <p class="font-italic small text-muted mb-0">
    - kokonaismassan ja omamassan välinen erotus (kantavuus) on vähintään 680 kg
  </p>
  <p class="font-italic small text-muted">
    - kantavuus alle 1000 kg ja tehon (kW) ja kokonaismassan (kg) osamäärä on
    enintään 0,05, tai kantavuus on vähintään 1000 kg ja tehon ja kokonaismassan
    osamäärä on enintään 0,06
  </p>

  <Tulosta />
</div>
