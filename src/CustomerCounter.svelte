<script>
  import { fly } from 'svelte/transition';
  export let settings;
  let currentCustomers = 0;
 
  let error;
  const showError = (errorName) => {
    while(true) {
      if(!error) break;
    }
    error = {
      name: errorName,
    };
    setTimeout(() => error = null, 3000);
  };

  const setCurrentCustomers = (num) => {
    if(currentCustomers + num > settings.maxCustomers)
      showError('Byl dosažen maximální počet zákazníků');
    if(currentCustomers + num >= 0 && currentCustomers + num <= settings.maxCustomers)
      currentCustomers += num;
  }

  let color = 'black';
  $: color = (currentCustomers / settings.maxCustomers < .5) ? 'green' : (currentCustomers / settings.maxCustomers < .75) ? 'orange' : 'red';
</script>

{#if error}
  <div class="error" transition:fly={{ x: window.innerWidth * 2, duration: 100}}>{error.name}</div>
{/if}
<div class='counter'>
	<div class="currentState" style='color: {color}'>{currentCustomers}</div>
	<div class="buttons">
    <div class='btn green' on:click={() => setCurrentCustomers(+1)}>+</div>
    <div class='btn red' on:click={() => setCurrentCustomers(-1)}>-</div>
  </div>
</div>

<style>
  * {
    font-size: 10rem;
    user-select: none;
  }
  .counter {
    box-sizing: border-box;
    height: 100vh;
    padding: .5rem;
    display: grid;
    grid-template-rows: auto auto;
  }
  .currentState {
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .buttons {
    display: grid;
    grid-template-columns: auto auto;
    column-gap: .5rem;
  }
  .btn {
    display: flex;
    justify-content: center;
    align-items: center;
    color: gainsboro
  }
  .green {
    background-color: green;
  }
  .red {
    background-color: red;
  }
  .error {
    position: absolute;
    right: 2vh;
    top: 2vh;
    font-size: 1rem;
    background-color: red;
    color: white;
    padding: .5rem;
    border-radius: .3rem;
  }
</style>