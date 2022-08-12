<script>
  import Tabs from "./Tabs.svelte";
  import Renkaat from "./renkaat.svelte";
  import CoAll from "./all_CO2.svelte";
  import Autovero from "./autovero.svelte";
  import Matkailuauto from "./matkailuauto.svelte";
  import Akselimassat from "./akselimassat.svelte";

  // List of tab items with labels and values.
  let tabItems = [
    { label: "Renkaat", value: 1 },
    { label: "CO₂", value: 2 },
    { label: "Autovero 8 §", value: 3 },
    { label: "Matkailuauto", value: 4 },
    { label: "Akselimassat", value: 5 }
  ];

  // Current active tab
  let currentTab = tabItems[0];

  window.onbeforeunload = function() {
    return "Haluatko varmasti poistua sivulta?";
  };
</script>

<Tabs bind:activeTabValue={currentTab} items={tabItems} />

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
