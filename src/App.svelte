<script>
  import Tabs from './Tabs.svelte';
  import Renkaat from './renkaat.svelte';
  import CoAll from './all_CO2.svelte';
  import Autovero from './autovero.svelte';
  import Matkailuauto from './matkailuauto.svelte';
  import Akselimassat from './akselimassat.svelte';

  let currentTab;

  window.onbeforeunload = function () {
    return 'Haluatko varmasti poistua sivulta?';
  };
</script>

<Tabs bind:activeTabValue={currentTab} />

{#if 1 === currentTab}
  <Renkaat />
{/if}

{#if 2 === currentTab}
  <CoAll />
{/if}

{#if 3 === currentTab}
  <Autovero />
{/if}

{#if 4 === currentTab}
  <Matkailuauto />
{/if}

{#if 5 === currentTab}
  <Akselimassat />
{/if}
