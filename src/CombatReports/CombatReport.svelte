<script>
	import Tdoll from "./Tdoll.svelte";
	import Fairy from "./Fairy.svelte";
	import Hoc from "./Hoc.svelte";

	let display = "t-doll";
</script>

<h1>Combat report calculator</h1>

<button on:click="{() => { display = "t-doll"}}" class:selected="{display == "t-doll"}">T-dolls</button>
<button on:click="{() => { display = "fairy"}}" class:selected="{display == "fairy"}">Fairies</button>
<button on:click="{() => { display = "hoc"}}" class:selected="{display == "hoc"}">HOCs</button>

{#if display == "t-doll"}
	<Tdoll />
{:else if display == "fairy"}
	<Fairy />
{:else if display == "hoc"}
	<Hoc />
{/if}

<style>
	h1 {
		color: #ff3e00;
		text-transform: uppercase;
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