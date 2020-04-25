<script>
	let currentLevel = 1;
	let targetLevel = 100;

	let xpByLevel = [
		0,
		300,
		900,
		1800,
		3000,
		4500,
		6300,
		8400,
		10800,
		13500,
		16500,
		19800,
		23400,
		27300,
		31500,
		36000,
		40800,
		45900,
		51400,
		57400,
		63900,
		71000,
		79000,
		88000,
		98000,
		109000,
		121200,
		134600,
		149300,
		165300,
		182800,
		201700,
		222200,
		244400,
		268300,
		294000,
		321600,
		351100,
		382700,
		416400,
		452300,
		490500,
		531000,
		574000,
		619500,
		667700,
		718600,
		772300,
		828900,
		888500,
		951200,
		1017100,
		1086300,
		1158900,
		1234900,
		1314500,
		1397800,
		1484800,
		1575700,
		1670600,
		1769600,
		1872700,
		1980100,
		2091900,
		2208200,
		2329100,
		2454700,
		2585100,
		2720400,
		2860800,
		3006300,
		3157100,
		3313200,
		3474800,
		3642000,
		3814900,
		3993600,
		4178300,
		4369000,
		4565900,
		4769100,
		4978700,
		5194800,
		5417600,
		5647200,
		5883700,
		6127200,
		6377800,
		6635700,
		6901000,
		7173800,
		7454200,
		7742400,
		8038500,
		8342600,
		8654900,
		8975500,
		9304500,
		9642000,
		9999000,
	];

	$: currentLevel = currentLevel > targetLevel ? targetLevel : currentLevel;
	$: levelDifference = targetLevel - currentLevel;
	$: xpToGain = (xpByLevel[targetLevel-1] - xpByLevel[currentLevel-1]);
	$: combatReports = Math.ceil(xpToGain / 3000);
</script>

<main>
	<div class="level-input">
		<h2>Current level</h2>
		<input type="number" min="1" max="100" bind:value={currentLevel} class="number">
		<input type="range" min="1" max="100" list="levels" bind:value={currentLevel} class="range">
	</div>
	
	<div class="level-input">
		<h2>Target level</h2>
		<input type="number" min="1" max="100" bind:value={targetLevel} class="number">
		<input type="range" min="1" max="100" list="levels" bind:value={targetLevel} class="range">
	</div>

	<datalist id="levels">
		<option value="1" label="1">
		<option value="20" label="20">
		<option value="40" label="40">
		<option value="70" label="70">
		<option value="100" label="100">
	</datalist>

	<hr>

	<p>Levels to gain: {levelDifference}</p>
	<p>XP to gain: {xpToGain}</p>
	<p class="reports">Combat reports: <b>{combatReports}</b></p>
</main>

<style>
	input {
		margin: auto;
		margin: 1rem;
	}

	h2 {
		font-size: 1.25rem;
	}

	.range {
		width: 500px;
	}

	.reports {
		font-size: 1.5rem;
	}
</style>