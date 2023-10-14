<script>
  import { onMount } from 'svelte';

  let items = [
    { label: 'Renkaat', value: 1 },
    { label: 'CO₂', value: 2 },
    { label: 'Autovero 8 §', value: 3 },
    { label: 'Matkailuauto', value: 4 },
    { label: 'Akselimassat', value: 5 },
  ];

  export let activeTabValue;

  onMount(() => {
    if (Array.isArray(items) && items.length && items[0].value) {
      activeTabValue = items[0].value;
    }
  });

  const handleClick = (tabValue) => () => (activeTabValue = tabValue);
</script>

<nav class="navbar navbar-expand-sm navbar-light bg-light border-bottom mb-2">
  <div class="logo">
    oktaani<strong>APU</strong>
  </div>
  <div class="nav-tabs-navigation">
    <div class="nav-tabs-wrapper">
      <ul class="nav nav-tabs">
        {#if Array.isArray(items)}
          {#each items as item}
            <li class="nav-item">
              <button
                class={activeTabValue === item.value ? 'nav-link active' : 'nav-link'}
                on:click={handleClick(item.value)}
              >
                {item.label}
              </button>
            </li>
          {/each}
        {/if}
      </ul>
    </div>
  </div>
</nav>

<style>
  .logo {
    margin-right: 2rem;
    font-size: 1.25rem;
  }

  .nav-tabs {
    border: 0;
    border-radius: 3px;
    padding: 0 15px;
  }

  .nav {
    display: flex;
    flex-wrap: wrap;
    padding-left: 0;
    margin-bottom: 0;
    list-style: none;
  }

  .nav-tabs .nav-item {
    margin-bottom: -1px;
  }

  .nav-tabs .nav-item .nav-link.active {
    background-color: #a9a9a9;
    transition: background-color 0.3s 0.2s;
  }

  .nav-tabs .nav-item .nav-link {
    border: 0 !important;
    color: #000 !important;
    font-weight: 500;
  }

  .nav-tabs .nav-item .nav-link {
    color: #000;
    border: 0;
    margin: 0;
    border-radius: 3px;
    line-height: 24px;
    text-transform: uppercase;
    font-size: 12px;
    padding: 7px 10px;
    background-color: transparent;
    transition: background-color 0.3s 0s;
  }

  .nav-link {
    display: block;
  }

  .nav .nav-item {
    position: relative;
  }

  @media (max-width: 575.98px) {
    .nav-tabs {
      margin-top: 10px;
    }
  }
</style>
