<script>
	import CombatReport from "./CombatReports/CombatReport.svelte";
	import Runs from "./Runs/Runs.svelte";
	import NeuralUpgrade from "./NeuralUpgrade.svelte";

	let menu = "combat-report";
</script>

<main>
	<nav>
		<button class="menu" on:click="{() => { menu = "combat-report" }}" class:selected={menu == "combat-report"}>Combat reports</button>
		<button class="menu" on:click="{() => { menu = "runs" }}" class:selected={menu == "runs"}>Runs</button>
		<button class="menu" on:click="{() => { menu = "neural-upgrade" }}" class:selected={menu == "neural-upgrade"}>Neural upgrade</button>
	</nav>

	{#if menu == "combat-report"}
		<CombatReport />
	{:else if menu == "runs"}
		<Runs />
	{:else if menu == "neural-upgrade"}
		<NeuralUpgrade />
	{/if}
</main>

<style>
	main {
		text-align: center;
		max-width: 240px;
		margin: 0 auto;
		font-size: 1.1rem;
	}

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

	nav {
		height: 3rem;
	}

	button:hover {
		background-color: #ff3e00;
		color: white;
		cursor: pointer;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>