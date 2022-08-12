<script>
  import Tulosta from "./tulosta.svelte";

  let etuakselimassa,
    takaakselimassa,
    omamassa,
    etuakseliOmamassa,
    takaakseliOmamassa,
    paikkalukuEtu,
    paikkalukuTaka,
    x1,
    x2,
    x3,
    paikkalukuEtuYht,
    paikkalukuTakaYht;

  //Omamassa yhteensä
  $: if (etuakseliOmamassa && takaakseliOmamassa) {
    omamassa = etuakseliOmamassa + takaakseliOmamassa;
  }

  //Akselimassat lasku
  $: if (
    paikkalukuEtu &&
    x1 &&
    x2 &&
    x3 &&
    paikkalukuTaka &&
    takaakseliOmamassa
  ) {
    paikkalukuEtuYht = paikkalukuEtu * 75;
    paikkalukuTakaYht = paikkalukuTaka * 75;

    takaakselimassa = (
      (paikkalukuEtuYht * x1 +
        paikkalukuTakaYht * (x1 + x2) +
        takaakseliOmamassa * (x1 + x2 + x3)) /
      (x1 + x2 + x3)
    ).toFixed(0);
    etuakselimassa = (
      omamassa +
      paikkalukuEtuYht +
      paikkalukuTakaYht -
      takaakselimassa
    ).toFixed(0);
  }
</script>

<style>
  .input-group-prepend span {
    width: 125px;
  }
  .etaisyys .input-group-prepend span {
    width: 270px;
  }
  .input-group-append span {
    width: 40px;
  }
</style>

<div class="container">

  <h2>Akselimassat</h2>
  <p class="lead">Laske akselimassat M1-luokan 2-akseliseen ajoneuvoon</p>

  <div class="row">
    <div class="col-md">

      <p class="mb-2">Omamassat</p>

      <div class="input-group input-group-sm mb-2">
        <div class="input-group-prepend">
          <span class="input-group-text">Etuakseli</span>
        </div>
        <input
          type="number"
          bind:value={etuakseliOmamassa}
          class="form-control"
          placeholder="Etuakseli" />
        <div class="input-group-append">
          <span class="input-group-text">kg</span>
        </div>
      </div>

      <div class="input-group input-group-sm mb-2">
        <div class="input-group-prepend">
          <span class="input-group-text">Taka-akseli</span>
        </div>
        <input
          type="number"
          bind:value={takaakseliOmamassa}
          class="form-control"
          placeholder="Taka-akseli" />
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
          class="form-control"
          placeholder={etuakseliOmamassa && takaakseliOmamassa ? omamassa : 'Omamassa yhteensä'}
          disabled />
        <div class="input-group-append">
          <span class="input-group-text">kg</span>
        </div>
      </div>

    </div>
    <div class="col-md">

      <p class="mb-2">Paikkaluku</p>

      <div class="input-group input-group-sm mb-2">
        <div class="input-group-prepend">
          <span class="input-group-text">Edessä</span>
        </div>
        <input
          type="number"
          bind:value={paikkalukuEtu}
          class="form-control"
          placeholder="Edessä" />
        <div class="input-group-append">
          <span class="input-group-text">kpl</span>
        </div>
      </div>

      <div class="input-group input-group-sm mb-2">
        <div class="input-group-prepend">
          <span class="input-group-text">Takana</span>
        </div>
        <input
          type="number"
          bind:value={paikkalukuTaka}
          class="form-control"
          placeholder="Takana" />
        <div class="input-group-append">
          <span class="input-group-text">kpl</span>
        </div>
      </div>

    </div>

  </div>

  <p class="mb-2">Etäisyydet</p>

  <div class="row">
    <div class="col-md-9">
      <div class="input-group input-group-sm mb-1 etaisyys">
        <div class="input-group-prepend">
          <span class="input-group-text">
            X1 - Etäisyys etuakseli -> etuistuimet
          </span>
        </div>
        <input
          type="number"
          bind:value={x1}
          class="form-control"
          placeholder="Etäisyys etuakseli -> etuistuimet" />
        <div class="input-group-append">
          <span class="input-group-text">m</span>
        </div>
      </div>

      <div class="input-group input-group-sm mb-1 etaisyys">
        <div class="input-group-prepend">
          <span class="input-group-text">
            X2 - Etäisyys etuistuimet -> takaistuimet
          </span>
        </div>
        <input
          type="number"
          bind:value={x2}
          class="form-control"
          placeholder="Etäisyys etuistuimet -> takaistuimet" />
        <div class="input-group-append">
          <span class="input-group-text">m</span>
        </div>
      </div>

      <div class="input-group input-group-sm mb-1 etaisyys">
        <div class="input-group-prepend">
          <span class="input-group-text">
            X3 - Etäisyys takaistuimet -> taka-akseli
          </span>
        </div>
        <input
          type="number"
          bind:value={x3}
          class="form-control"
          placeholder="Etäisyys takaistuimet -> taka-akseli" />
        <div class="input-group-append">
          <span class="input-group-text">m</span>
        </div>
      </div>
    </div>
    <div class="col-md-3 text-center">
      <img src="img/car.png" height="100px" alt="Mitat" />
    </div>
  </div>

  <p class="mb-2">Akselimassat</p>

  <div class="row">
    <div class="col-md">

      <div class="input-group input-group-sm mb-1">
        <div class="input-group-prepend">
          <span class="input-group-text alert-success">Etuakseli</span>
        </div>
        <input
          type="number"
          class="form-control"
          placeholder={etuakselimassa ? etuakselimassa : 'Täytä kaikki kentät'}
          disabled />
        <div class="input-group-append">
          <span class="input-group-text">kg</span>
        </div>
      </div>
    </div>
    <div class="col-md">
      <div class="input-group input-group-sm mb-1">
        <div class="input-group-prepend">
          <span class="input-group-text alert-success">Taka-akseli</span>
        </div>
        <input
          type="number"
          class="form-control"
          placeholder={takaakselimassa ? takaakselimassa : 'Täytä kaikki kentät'}
          disabled />
        <div class="input-group-append">
          <span class="input-group-text">kg</span>
        </div>
      </div>
    </div>
  </div>

  <Tulosta />

</div>
