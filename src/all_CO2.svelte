<script>
  import Tulosta from './tulosta.svelte';
  import BmCO2 from './CO2/bm_CO2.svelte';
  import BaCO2 from './CO2/ba_CO2.svelte';
  import BsCO2 from './CO2/bs_CO2.svelte';
  import DmCO2 from './CO2/dm_CO2.svelte';
  import DaCO2 from './CO2/da_CO2.svelte';
</script>

<div class="container">
  <h2>CO&#8322;</h2>
  <p class="lead">CO&#8322;-päästöjen arvioinnissa käytetään seuraavia laskukaavoja.</p>

  <BmCO2 />
  <BaCO2 />
  <BsCO2 />
  <DmCO2 />
  <DaCO2 />

  <p class="font-italic small text-muted mb-0">
    Missä CO&#8322; on CO&#8322;-päästöjen yhdistetty massa (g/km), m on ajokuntoisen ajoneuvon massa (kg) ja p on
    moottorin enimmäislähtöteho (kW).
  </p>
  <p class="font-italic small text-muted mb-0">
    CO&#8322;:n yhdistetty massa lasketaan yhden desimaalin tarkkuudella ja pyöristetään sitten lähimpään kokonaislukuun
    seuraavasti:
  </p>
  <p class="font-italic small text-muted mb-0">
    a) jos desimaalipilkun jälkeen tuleva luku on pienempi kuin 5, pyöristetään alaspäin
  </p>
  <p class="font-italic small text-muted">
    b) jos desimaalipilkun jälkeen tuleva luku on 5 tai suurempi kuin 5, pyöristetään ylöspäin.
  </p>

  <Tulosta />
</div>
