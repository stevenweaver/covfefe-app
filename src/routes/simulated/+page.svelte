<script>
	import { onMount, beforeUpdate } from 'svelte';
	import { Runtime, Inspector } from '@observablehq/runtime';
	import notebook from '921402678226d2da';

	let notebookRef;
	let variableNames = [];

	onMount(async () => {

	});

</script>

<div class="container">
  <h1>Simulated Data</h1>

</div>

<style>
	:global(.container h1) {
		@apply text-xxl font-semibold;
		font-size: xx-large;
		margin-top: 15px;
		margin-bottom: 15px;
	}

	:global(#data) {
		display: none;
	}
</style>
