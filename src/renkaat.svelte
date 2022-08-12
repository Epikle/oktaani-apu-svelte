<script>
  import Tulosta from "./tulosta.svelte";

  let etuakseli, taka_akseli, leveys, halkaisija, vierintakeha;
  let leveysNew, halkaisijaNew, vierintakehaNew, kantavuusNew;
  let leveysMuutos,
    halkaisijaMuutos,
    halkaisijaMuutosP,
    vierintakehaMuutos,
    kantavuusetuMuutos,
    kantavuustakaMuutos;
  let leveysTakaMuutos, halkaisijaTakaMuutos, vierintakehaTakaMuutos;
  let leveysTaka, halkaisijaTaka, vierintakehaTaka;
  let leveysTakaNew, halkaisijaTakaNew, vierintakehaTakaNew, kantavuusTakaNew;

  let laske = false;
  let laskeTaka = false;
  let laskeNew = false;
  let laskeTakaNew = false;
  let rengaskootTyyppi = true;
  let rengaskootNew = true;

  $: if (!rengaskootNew && rengaskootTyyppi) {
    leveysTaka = leveys;
    halkaisijaTaka = halkaisija;
    vierintakehaTaka = vierintakeha;
  }

  //Kantavuus etuakselille
  $: if (kantavuusNew && etuakseli) {
    if (kantavuusNew * 2 >= etuakseli) {
      kantavuusetuMuutos = "RIITTÄÄ, " + kantavuusNew * 2 + " kg";
    } else {
      kantavuusetuMuutos = "EI RIITÄ, " + kantavuusNew * 2 + " kg";
    }
  }

  //Kantavuus taka-akselille
  $: if (kantavuusNew && taka_akseli && rengaskootNew) {
    if (kantavuusNew * 2 >= taka_akseli) {
      kantavuustakaMuutos = "RIITTÄÄ, " + kantavuusNew * 2 + " kg";
    } else {
      kantavuustakaMuutos = "EI RIITÄ, " + kantavuusNew * 2 + " kg";
    }
  } else if (kantavuusNew && taka_akseli && !rengaskootNew) {
    if (kantavuusTakaNew * 2 >= taka_akseli) {
      kantavuustakaMuutos = "RIITTÄÄ, " + kantavuusTakaNew * 2 + " kg";
    } else {
      kantavuustakaMuutos = "EI RIITÄ, " + kantavuusTakaNew * 2 + " kg";
    }
  }

  //Renkaan leveys
  $: if (leveys && leveysNew) {
    leveysMuutos = Math.abs(leveys - leveysNew);
  }

  //Renkaan leveys monta
  $: if (leveysTaka && leveysTakaNew) {
    leveysTakaMuutos = Math.abs(leveysTaka - leveysTakaNew);
  }

  //Renkaan halkaisija muutos
  $: if (halkaisija && halkaisijaNew) {
    halkaisijaMuutos =
      Math.abs(halkaisija - halkaisijaNew).toFixed(2) +
      " mm / " +
      Math.abs((halkaisijaNew / halkaisija) * 100 - 100).toFixed(2) +
      " %";
  }

  //Renkaan halkaisija muutos monta
  $: if (halkaisijaTaka && halkaisijaTakaNew) {
    halkaisijaTakaMuutos =
      Math.abs(halkaisijaTaka - halkaisijaTakaNew).toFixed(2) +
      " mm / " +
      Math.abs((halkaisijaTakaNew / halkaisijaTaka) * 100 - 100).toFixed(2) +
      " %";
  }

  //Tyyppihyväksytyn renkaan vierintäkehä
  $: if (laske && halkaisija) {
    vierintakeha = (halkaisija * Math.PI).toFixed(0);
  }

  $: if (laskeTaka && halkaisijaTaka) {
    vierintakehaTaka = (halkaisijaTaka * Math.PI).toFixed(0);
  }

  //Uuden renkaan vierintäkehä
  $: if (laskeNew && halkaisijaNew) {
    vierintakehaNew = (halkaisijaNew * Math.PI).toFixed(0);
  }

  $: if (laskeTakaNew && halkaisijaTakaNew) {
    vierintakehaTakaNew = (halkaisijaTakaNew * Math.PI).toFixed(0);
  }

  //Vierintäkehän muutos
  $: if (vierintakeha && vierintakehaNew) {
    vierintakehaMuutos = Math.abs(
      (vierintakehaNew / vierintakeha) * 100 - 100
    ).toFixed(2);
  }

  //Vierintäkehän muutos monta
  $: if (vierintakehaTaka && vierintakehaTakaNew) {
    vierintakehaTakaMuutos = Math.abs(
      (vierintakehaTakaNew / vierintakehaTaka) * 100 - 100
    ).toFixed(2);
  }

  $: if (rengaskootNew) {
    rengaskootTyyppi = true;
  }
</script>

<style>
  .input-group-prepend span {
    width: 125px;
  }
  .renkaatpre .input-group-prepend span {
    width: 100px;
  }
  .input-group-append span {
    width: 40px;
  }

  @media print {
    .badge {
      padding: 2px 6px;
      border: none;
    }
  }
</style>

<div class="container">

  <h2>Renkaat</h2>
  <p class="lead">Rengas- ja/tai vannekoon muuttaminen</p>

  <div class="row">
    <div class="col-md">
      <p class="mb-2">Perustiedot</p>
      <div class="input-group input-group-sm mb-2">
        <div class="input-group-prepend">
          <span class="input-group-text">Rekisterinumero</span>
        </div>
        <input type="text" class="form-control" placeholder="Rekisterinumero" />
      </div>

      <div class="input-group input-group-sm mb-2">
        <div class="input-group-prepend">
          <span class="input-group-text">Valmistenumero</span>
        </div>
        <input type="text" class="form-control" placeholder="Valmistenumero" />
      </div>
    </div>
    <div class="col-md">

      <p class="mb-2">Akselimassat</p>
      <div class="input-group input-group-sm mb-2">
        <div class="input-group-prepend">
          <span class="input-group-text">Etuakseli</span>
        </div>
        <input
          type="number"
          bind:value={etuakseli}
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
          bind:value={taka_akseli}
          class="form-control"
          placeholder="Taka-akseli" />
        <div class="input-group-append">
          <span class="input-group-text">kg</span>
        </div>
      </div>
    </div>
  </div>

  <p class="my-2">
    Tyyppihyväksytty rengas
    {#if !rengaskootNew}
      <span class="badge badge-secondary mr-1">Samankokoiset renkaat</span>
      <input type="checkbox" bind:checked={rengaskootTyyppi} />
    {/if}
  </p>
  <div class="row renkaatpre">
    <div class="col-md">
      {#if !rengaskootTyyppi}
        <span class="badge badge-secondary mb-2">ETUAKSELI</span>
      {/if}
      <div class="input-group input-group-sm mb-2">
        <div class="input-group-prepend">
          <span class="input-group-text">Rengas</span>
        </div>
        <input type="text" class="form-control" placeholder="Rengas" />
      </div>

      <div class="input-group input-group-sm mb-2">
        <div class="input-group-prepend">
          <span class="input-group-text">Leveys</span>
        </div>
        <input
          type="number"
          bind:value={leveys}
          class="form-control"
          placeholder="Leveys (renkaasta)" />
        <div class="input-group-append">
          <span class="input-group-text">mm</span>
        </div>
      </div>

      <div class="input-group input-group-sm mb-2">
        <div class="input-group-prepend">
          <span class="input-group-text">Halkaisija</span>
        </div>
        <input
          type="number"
          bind:value={halkaisija}
          class="form-control"
          placeholder="Halkaisija (STRO)" />
        <div class="input-group-append">
          <span class="input-group-text">mm</span>
        </div>
      </div>

      <div class="input-group input-group-sm mb-2">
        <div class="input-group-prepend">
          <span class="input-group-text">Vierintäkehä</span>
        </div>
        <input
          type="number"
          bind:value={vierintakeha}
          class="form-control"
          placeholder="Vierintäkehä (STRO/laskemalla)"
          disabled={laske} />
        <div class="input-group-append">
          <div class="input-group-text">
            <span class="badge badge-secondary mr-2">LASKE</span>
            <input type="checkbox" bind:checked={laske} />
          </div>
          <span class="input-group-text">mm</span>
        </div>
      </div>
    </div>
    {#if !rengaskootTyyppi}
      <div class="col-md">
        <span class="badge badge-secondary mb-2">TAKA-AKSELI</span>
        <div class="input-group input-group-sm mb-2">
          <div class="input-group-prepend">
            <span class="input-group-text">Rengas</span>
          </div>
          <input type="text" class="form-control" placeholder="Rengas" />
        </div>

        <div class="input-group input-group-sm mb-2">
          <div class="input-group-prepend">
            <span class="input-group-text">Leveys</span>
          </div>
          <input
            type="number"
            bind:value={leveysTaka}
            class="form-control"
            placeholder="Leveys (renkaasta)" />
          <div class="input-group-append">
            <span class="input-group-text">mm</span>
          </div>
        </div>

        <div class="input-group input-group-sm mb-2">
          <div class="input-group-prepend">
            <span class="input-group-text">Halkaisija</span>
          </div>
          <input
            type="number"
            bind:value={halkaisijaTaka}
            class="form-control"
            placeholder="Halkaisija (STRO)" />
          <div class="input-group-append">
            <span class="input-group-text">mm</span>
          </div>
        </div>

        <div class="input-group input-group-sm mb-2">
          <div class="input-group-prepend">
            <span class="input-group-text">Vierintäkehä</span>
          </div>
          <input
            type="number"
            bind:value={vierintakehaTaka}
            class="form-control"
            placeholder="Vierintäkehä (STRO/laskemalla)"
            disabled={laskeTaka} />
          <div class="input-group-append">
            <div class="input-group-text">
              <span class="badge badge-secondary mr-2">LASKE</span>
              <input type="checkbox" bind:checked={laskeTaka} />
            </div>
            <span class="input-group-text">mm</span>
          </div>
        </div>
      </div>
    {/if}
  </div>
  <p class="my-2">
    Uusi rengas
    <span class="badge badge-secondary mr-1">Samankokoiset renkaat</span>
    <input type="checkbox" bind:checked={rengaskootNew} />
  </p>
  <div class="row renkaatpre">
    <div class="col-md">
      {#if !rengaskootNew}
        <span class="badge badge-secondary mb-2">ETUAKSELI</span>
      {/if}
      <div class="input-group input-group-sm mb-2">
        <div class="input-group-prepend">
          <span class="input-group-text">Rengas</span>
        </div>
        <input type="text" class="form-control" placeholder="Rengas" />
      </div>

      <div class="input-group input-group-sm mb-2">
        <div class="input-group-prepend">
          <span class="input-group-text">Leveys</span>
        </div>
        <input
          type="number"
          bind:value={leveysNew}
          class="form-control"
          placeholder="Leveys (renkaasta)" />
        <div class="input-group-append">
          <span class="input-group-text">mm</span>
        </div>
      </div>

      <div class="input-group input-group-sm mb-2">
        <div class="input-group-prepend">
          <span class="input-group-text">Halkaisija</span>
        </div>
        <input
          type="number"
          bind:value={halkaisijaNew}
          class="form-control"
          placeholder="Halkaisija (STRO)" />
        <div class="input-group-append">
          <span class="input-group-text">mm</span>
        </div>
      </div>

      <div class="input-group input-group-sm mb-2">
        <div class="input-group-prepend">
          <span class="input-group-text">Vierintäkehä</span>
        </div>
        <input
          type="number"
          bind:value={vierintakehaNew}
          class="form-control"
          placeholder="Vierintäkehä (STRO/laskemalla)"
          disabled={laskeNew} />
        <div class="input-group-append">
          <div class="input-group-text">
            <span class="badge badge-secondary mr-2">LASKE</span>
            <input type="checkbox" bind:checked={laskeNew} />
          </div>
          <span class="input-group-text">mm</span>
        </div>
      </div>

      <div class="input-group input-group-sm mb-2">
        <div class="input-group-prepend">
          <span class="input-group-text">Kantavuus</span>
        </div>
        <input
          type="number"
          bind:value={kantavuusNew}
          class="form-control"
          placeholder="Kantavuus (renkaasta/STRO)" />
        <div class="input-group-append">
          <span class="input-group-text">kg</span>
        </div>
      </div>
    </div>
    {#if !rengaskootNew}
      <div class="col-md">
        <span class="badge badge-secondary mb-2">TAKA-AKSELI</span>
        <div class="input-group input-group-sm mb-2">
          <div class="input-group-prepend">
            <span class="input-group-text">Rengas</span>
          </div>
          <input type="text" class="form-control" placeholder="Rengas" />
        </div>

        <div class="input-group input-group-sm mb-2">
          <div class="input-group-prepend">
            <span class="input-group-text">Leveys</span>
          </div>
          <input
            type="number"
            bind:value={leveysTakaNew}
            class="form-control"
            placeholder="Leveys (renkaasta)" />
          <div class="input-group-append">
            <span class="input-group-text">mm</span>
          </div>
        </div>

        <div class="input-group input-group-sm mb-2">
          <div class="input-group-prepend">
            <span class="input-group-text">Halkaisija</span>
          </div>
          <input
            type="number"
            bind:value={halkaisijaTakaNew}
            class="form-control"
            placeholder="Halkaisija (STRO)" />
          <div class="input-group-append">
            <span class="input-group-text">mm</span>
          </div>
        </div>

        <div class="input-group input-group-sm mb-2">
          <div class="input-group-prepend">
            <span class="input-group-text">Vierintäkehä</span>
          </div>
          <input
            type="number"
            bind:value={vierintakehaTakaNew}
            class="form-control"
            placeholder="Vierintäkehä (STRO/laskemalla)"
            disabled={laskeTakaNew} />
          <div class="input-group-append">
            <div class="input-group-text">
              <span class="badge badge-secondary mr-2">LASKE</span>
              <input type="checkbox" bind:checked={laskeTakaNew} />
            </div>
            <span class="input-group-text">mm</span>
          </div>
        </div>

        <div class="input-group input-group-sm mb-2">
          <div class="input-group-prepend">
            <span class="input-group-text">Kantavuus</span>
          </div>
          <input
            type="number"
            bind:value={kantavuusTakaNew}
            class="form-control"
            placeholder="Kantavuus (renkaasta/STRO)" />
          <div class="input-group-append">
            <span class="input-group-text">kg</span>
          </div>
        </div>
      </div>
    {/if}
  </div>

  <p class="my-2">Muutos</p>

  <div class="row">

    <div class="col-md">

      <div class="input-group input-group-sm mb-2">
        <div class="input-group-prepend">
          <span class="input-group-text alert-success">Etuakselimassa</span>
        </div>
        <input
          type="text"
          class="form-control"
          placeholder={kantavuusNew && etuakseli ? kantavuusetuMuutos : 'Etuakseli'}
          disabled />
      </div>
    </div>

    <div class="col-md">
      <div class="input-group input-group-sm mb-2">
        <div class="input-group-prepend">
          <span class="input-group-text alert-success">Taka-akselimassa</span>
        </div>
        <input
          type="text"
          class="form-control"
          placeholder={kantavuusNew && taka_akseli ? kantavuustakaMuutos : 'Taka-akseli'}
          disabled />
      </div>
    </div>

    <div class="col-12">
      <small class="form-text text-muted mb-2 mt-0">
        Tarkasta renkaiden merkinnöistä ja STRO- tiedoista, että renkaiden
        kantavuus on riittävä rekisteritietoihin merkityille akselimassoille.
      </small>
    </div>
  </div>

  <div class="row">
    <div class="col-md">
      {#if !rengaskootNew}
        <span class="badge badge-secondary mb-2">ETUAKSELI</span>
      {/if}
      <div class="input-group input-group-sm mb-2">
        <div class="input-group-prepend">
          <span class="input-group-text alert-success">Leveys</span>
        </div>
        <input
          type="number"
          class="form-control"
          placeholder={leveysNew && leveys ? leveysMuutos : 'Leveys'}
          disabled />
        <div class="input-group-append">
          <span class="input-group-text">mm</span>
        </div>
      </div>
    </div>
    {#if !rengaskootNew}
      <div class="col-md">

        <span class="badge badge-secondary mb-2">TAKA-AKSELI</span>

        <div class="input-group input-group-sm mb-2">
          <div class="input-group-prepend">
            <span class="input-group-text alert-success">Leveys</span>
          </div>
          <input
            type="number"
            class="form-control"
            placeholder={leveysTakaNew && leveysTaka ? leveysTakaMuutos : 'Leveys'}
            disabled />
          <div class="input-group-append">
            <span class="input-group-text">mm</span>
          </div>
        </div>
      </div>
    {/if}

    <div class="col-12">
      <small class="form-text text-muted mb-2 mt-0">
        Muutoskatsastuksessa voidaan hyväksyä renkaan leveyden muuttaminen
        ajoneuvon valmistelijan ilmoittamaan leveimpään renkaaseen nähden
        enintään 50 prosenttia tai 105 millimetriä suuremman arvoista ollessa
        määräävä.
        <br />
        Vanteiden vaihdon seurauksena ajoneuvon kunkin akseliston raideväli saa
        muuttua enintään 30 millimetriä alkuperäiseen verrattuna, ellei
        ajoneuvon valmistaja muuta ilmoita. Vanteiden on oltava pyörännapoihin
        ja akselimassoille sopivat.
      </small>
    </div>

  </div>

  <div class="row">
    <div class="col-md">
      {#if !rengaskootNew}
        <span class="badge badge-secondary mb-2">ETUAKSELI</span>
      {/if}

      <div class="input-group input-group-sm mb-2">
        <div class="input-group-prepend">
          <span class="input-group-text alert-success">Halkaisija</span>
        </div>
        <input
          type="text"
          class="form-control"
          placeholder={halkaisija && halkaisijaNew ? halkaisijaMuutos : 'Halkaisija'}
          disabled />
      </div>
    </div>

    {#if !rengaskootNew}
      <div class="col-md">

        <span class="badge badge-secondary mb-2">TAKA-AKSELI</span>

        <div class="input-group input-group-sm mb-2">
          <div class="input-group-prepend">
            <span class="input-group-text alert-success">Halkaisija</span>
          </div>
          <input
            type="text"
            class="form-control"
            placeholder={halkaisijaTaka && halkaisijaTakaNew ? halkaisijaTakaMuutos : 'Halkaisija'}
            disabled />
        </div>

      </div>
    {/if}

    <div class="col-12">
      <small class="form-text text-muted mb-2 mt-0">
        Renkaan ulkohalkaisijaa saa muuttaa ajoneuvon valmistajan ilmoittamaan
        suurimpaan renkaaseen verrattuna enintään 15 prosenttia. Muutettaessa
        renkaan ulkohalkaisijaa, on mahdolliset nopeudenrajoitin ja ajopiirturi
        kalibroitava sekä nopeusmittarin näyttämä tarvittaessa korjattava. Jos
        ylittyy niin poikkeuslupa.
      </small>
    </div>

  </div>

  <div class="row">
    <div class="col-md">
      {#if !rengaskootNew}
        <span class="badge badge-secondary mb-2">ETUAKSELI</span>
      {/if}

      <div class="input-group input-group-sm mb-2">
        <div class="input-group-prepend">
          <span class="input-group-text alert-success">Vierintäkehä</span>
        </div>
        <input
          type="number"
          class="form-control"
          placeholder={vierintakeha && vierintakehaNew ? vierintakehaMuutos : 'Vierintäkehä'}
          disabled />
        <div class="input-group-append">
          <span class="input-group-text">%</span>
        </div>
      </div>

    </div>

    {#if !rengaskootNew}
      <div class="col-md">

        <span class="badge badge-secondary mb-2">TAKA-AKSELI</span>

        <div class="input-group input-group-sm mb-2">
          <div class="input-group-prepend">
            <span class="input-group-text alert-success">Vierintäkehä</span>
          </div>
          <input
            type="number"
            class="form-control"
            placeholder={vierintakehaTaka && vierintakehaTakaNew ? vierintakehaTakaMuutos : 'Vierintäkehä'}
            disabled />
          <div class="input-group-append">
            <span class="input-group-text">%</span>
          </div>
        </div>

      </div>
    {/if}

    <div class="col-12">
      <small class="form-text text-muted mb-2 mt-0">
        Jos muutoskatsastuksessa renkaan vierintäkehä muuttuu yli 5 %
        alkuperäiseen vierintäkehään verrattuna, tulee nopeusmittarin näyttämä
        tarkistaa. Sallitut poikkeamat löytyvät E-säännöstä N:o 39.
        <br />
        Todellinen nopeus voidaan todeta luotettavalla ulkoisella
        mittalaitteella (tutkalla mittaamalla tai GPS-paikannukseen perustuvalla
        mittalaitteella ts. navigaattorilla).
      </small>
    </div>

  </div>

  <Tulosta />
</div>
