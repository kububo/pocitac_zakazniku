<script>
	import CustomerCounter from './CustomerCounter.svelte';
	import Settings from './Settings.svelte';
	
	let settings;
</script>

{#if !settings}
	<Settings bind:settings={settings} />
{:else}
	<CustomerCounter settings={settings} />
{/if}