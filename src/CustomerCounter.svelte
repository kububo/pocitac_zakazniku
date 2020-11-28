<script>
  export let maxCustomers;
  let currentCustomers = 0;

  const setCurrentCustomers = (num) => {
    if(currentCustomers + num >= 0 && currentCustomers + num <= maxCustomers)
      currentCustomers += num;
  }

  let color = 'black';
  $: color = (currentCustomers / maxCustomers < .5) ? 'green' : (currentCustomers / maxCustomers < .75) ? 'orange' : 'red';
</script>

<div class='counter'>
	<div class="currentState" style='color: {color}'>{currentCustomers}</div>
	<div class="buttons">
    <button class='red' on:click={() => setCurrentCustomers(+1)}>+</button>
    <button class='green' on:click={() => setCurrentCustomers(-1)}>-</button>
  </div>
</div>

<style>
  * {
    font-size: 10rem;
  }
  .counter {
    box-sizing: border-box;
    height: 100vh;
    padding: 2rem;
    display: grid;
    grid-template-rows: auto auto;
  }
  .currentState {
    display: flex;
    justify-content: center;
    align-self: center;
  }
</style>