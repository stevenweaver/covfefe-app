<script>
	import { onMount, beforeUpdate } from 'svelte';
	import { Runtime, Inspector } from '@observablehq/runtime';
	import notebook from '921402678226d2da';

	let notebookRef;
	let variableNames = [];
	let viewFlag = false;

	onMount(async () => {

		const runtime = new Runtime();

		let main = runtime.module(notebook, (name) => {

			const node = Inspector.into(notebookRef)(name);

			variableNames.push(name);

      if(name == 'overview') {
        viewFlag = true;
      }

			if (name == 'simDataHeader') {
				viewFlag = false;
			}

			if (viewFlag) {
				// Once we reach the "data" name, turn off appending

				// if (name == 'viewof table1') {
				// 	node._node.classList.add('table');
				// 	node._node.classList.add('table-striped');
				// }

				return node;
			} else {
				return null;
			}

		});

	});

</script>

<div class="container">
  <h1>Overview</h1>
  <div class="overview" bind:this={notebookRef}></div>
</div>

<style>

	:global(.container h1) {
		@apply text-xxl font-semibold;
		font-size: xx-large;
		margin-top: 15px;
		margin-bottom: 15px;
	}

	:global(.container h2) {
		margin-top: 20px;
		margin-bottom: 20px;
	}

	:global(.container svg) {
		display: inline;
	}


	:global(.container table) {
		width: 100%;
    margin-top: 10px;
		border-collapse: collapse;
		@apply shadow-md rounded-lg;  /* Add shadow and rounded corners */
	}

	:global(.container th) {
		background-color: #f3f4f6;  /* Light grey background */
		@apply py-2 px-4 text-left border-b;  /* Padding and border */
	}

	:global(.container td) {
		@apply py-2 px-4 text-left border-b;  /* Padding and border */
	}

	:global(#data) {
		display: none;
	}

</style>

