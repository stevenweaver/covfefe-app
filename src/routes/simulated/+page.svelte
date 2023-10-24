<script>
	import { onMount, beforeUpdate } from 'svelte';
	import { Runtime, Inspector } from '@observablehq/runtime';
	import notebook from '921402678226d2da';

	let notebookRef;
	let variableNames = [];
	let viewFlag = false;
	let hideFlag = false;

	onMount(async () => {

		const runtime = new Runtime();

		let main = runtime.module(notebook, (name) => {

			const node = Inspector.into(notebookRef)(name);

			variableNames.push(name);

      if(name == 'simDataOverview') {
        viewFlag = true;
      }

			if (name == 'empiricalResultsHeader') {
				viewFlag = false;
			}

      if( name == 'reports') {
        viewFlag = true;
        hideFlag = true;
      }

			if (viewFlag) {
				// Once we reach the "data" name, turn off appending

				// if (name == 'viewof table1') {
				// 	node._node.classList.add('table');
				// 	node._node.classList.add('table-striped');
				// }
        if(hideFlag) {
          node._node.style.display = 'none';
        }
				return node;
			} else {
				return null;
			}

		});



	});

</script>

<div class="container">
  <h1>Simulations</h1>
  <div class="simulated" bind:this={notebookRef}></div>
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

  :global(input[type=range]) {
  -webkit-appearance: none;  /* Remove default styling */
  width: 100%;
  height: 10px;  /* Height of the slider */
  border-radius: 5px;
  background: #ddd;
}

:global(input[type=range]::-webkit-slider-thumb) {
  -webkit-appearance: none;
  width: 20px;  /* Width of the slider handle */
  height: 20px;  /* Height of the slider handle */
  background: #007bff;  /* Background color */
  cursor: pointer;  /* Cursor on hover */
  border-radius: 50%;  /* Rounded corners */
}

:global(input[type=range]::-moz-range-thumb) {
  width: 20px;
  height: 20px;
  background: #007bff;
  cursor: pointer;
  border-radius: 50%;
}

:global(select) {
  width: 100%;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
  appearance: none; /* Remove default appearance */
  background-color: #fff;
  background-image: url('data:image/svg+xml;utf8,<svg viewBox="0 0 24 24" fill="black" xmlns="http://www.w3.org/2000/svg"><path d="M7 10l5 5 5-5H7z"/></svg>');
  background-repeat: no-repeat;
  background-position: right 10px center;
}

:global(select:focus) {
  outline: none;
  border-color: #5c6bc0;
}

:global(.container h3) {
  margin-top: 15px;
  margin-bottom: 15px;
  font-size: large;
  font-weight: bold;
  text-transform: uppercase;
  letter-spacing: 1px;
  color: #333;
}


:global(.container h4) {
  margin-top: 15px;
  margin-bottom: 15px;
  font-size: medium;
  font-weight: bold;
  text-transform: uppercase;
  letter-spacing: 1px;
  color: #333;
}


</style>

