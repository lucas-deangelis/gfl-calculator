<script>
  import ZeroTwo from "./ZeroTwo.svelte";
  import SixOneN from "./SixOneN.svelte";
  import EightOneN from "./EightOneN.svelte";

	let display = "0-2";
</script>

<h1>{display} RUNS CALCULATOR</h1>

<button on:click="{() => { display = "0-2"}}" class:selected="{display == "0-2"}">0-2</button>
<button on:click="{() => { display = "6-3n"}}" class:selected="{display == "6-3n"}">6-3n</button>
<button on:click="{() => { display = "8-1n"}}" class:selected="{display == "8-1n"}">8-1n</button>

{#if display == "0-2"}
  <ZeroTwo />
{:else if display == "6-3n"}
  <SixOneN />
{:else if display == "8-1n"}
  <EightOneN />
{/if}

<style>
	h1 {
		color: #ff3e00;
		font-size: 3.5em;
		font-weight: 100;
		margin-top: 1.5rem;
		margin-bottom: 1.5rem;
	}

	.selected {
		background-color: #ff3e00;
		color: white;
	}

	button:hover {
		background-color: #ff3e00;
		color: white;
		cursor: pointer;
	}
</style>