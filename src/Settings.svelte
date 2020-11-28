<script>
  export let settings;
  let settingsCache = {
    maxCustomers: 0
  };
  $: {
    if(settingsCache.maxCustomers < 0)
      settingsCache.maxCustomers = 0;
  }
</script>

<div class='settings'>
  <h1>Nastavení</h1>
  <div class='line'>
    <label for="maxCustomer">Maximální počet zákazníků</label>
    <input type="number" id='maxCustomers' bind:value={settingsCache.maxCustomers}>
  </div>
  <div class='line'>
    <label for="apiURL">
      <span>API URL</span>
      <span class="small">volitelné</span>
    </label>
    <input type="text" id='apiURL' placeholder="http://" bind:value={settingsCache.apiURL}>
  </div>
  <button on:click={() => settings = settingsCache}>Uložit</button>
</div>

<style>
  .settings {
    box-sizing: border-box;
    padding: 1rem;
    display: flex;
    flex-direction: column;
    min-height: 100vh;
  }
  .line {
    display: flex;
    flex-direction: column;
    margin: .75rem 0;
  }
  .small {
    font-size: 75%;
    color: gray;
  }
  button {
    margin-top: auto;
    border: 1px solid darkblue;
    background-color: #273469;
    color: gainsboro;
    height: 3rem;
    font-size: 1.5rem;
  }
</style>