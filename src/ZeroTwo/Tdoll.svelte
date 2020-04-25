<script>
	let currentLevel = 1;
	let targetLevel = 90;
	let oathed = false;
	let info = false;
	let event = false;
	let command = false;
	let leader = false;
	let MVP = false;

	let xpByLevel = [
		0,
		0,
		100,
		300,
		600,
		1000,
		1500,
		2100,
		2800,
		3600,
		4500,
		5500,
		6600,
		7800,
		9100,
		10500,
		12000,
		13600,
		15300,
		17100,
		19000,
		21000,
		23100,
		25300,
		27600,
		30000,
		32500,
		35100,
		37900,
		41000,
		44400,
		48600,
		53200,
		58200,
		63600,
		69400,
		75700,
		82400,
		89600,
		97300,
		105500,
		114300,
		123600,
		133500,
		144000,
		155100,
		166900,
		179400,
		192500,
		206400,
		221000,
		236400,
		252500,
		269400,
		287100,
		305700,
		325200,
		345600,
		366900,
		389200,
		412500,
		436800,
		462100,
		488400,
		515800,
		544300,
		573900,
		604700,
		636700,
		669900,
		704300,
		749400,
		796200,
		844800,
		895200,
		947400,
		1001400,
		1057300,
		1115200,
		1175000,
		1236800,
		1300700,
		1366700,
		1434800,
		1505100,
		1577700,
		1652500,
		1729600,
		1809100,
		1891000,
		1975300,
		2087900,
		2204000,
		2323500,
		2446600,
		2573300,
		2703700,
		2837800,
		2975700,
		3117500,
		3263200,
		3363200,
		3483200,
		3623200,
		3783200,
		3963200,
		4163200,
		4383200,
		4623200,
		4903200,
		5263200,
		5743200,
		6383200,
		7283200,
		8483200,
		10083200,
		12283200,
		15283200,
		19283200,
		24283200,
		30283200,
	];

	function xpUnder100(current, target) {
		return xpByLevel[target] - xpByLevel[current];
	}

	function xpOver100(current, target, oath) {
		if (oath) {
			return xpUnder100(current, target) / 2;
		} else {
			return xpUnder100(current, target);
		}
	}

	function xpIfOathed(current, target, oath) {
		if (current >= target) {
			return 0;
		} else if (target > 100 && current < 100) {
			return xpUnder100(current, 100) + xpOver100(100, target, oath);
		} else if (target <= 100) {
			return xpUnder100(current, target);
		} else if (current >= 100) {
			return xpOver100(current, target, oath);
		}
	}

	function zip(arrays) {
		return arrays[0].map(function(_, i) {
			return arrays.map(function(array) {
				return array[i];
			});
		});
	}

	function runsNb(current, target, oath, event, command, leader, MVP) {
		let levelsCurrent = [1, 10, 30, 70, 90].map(l => (l < current ? current : l));
		let levelsTarget = [10, 30, 70, 90, 120].map(l => (l < target ? l : target));
		let buff = 1 * (event ? 1.5 : 1) * (command ? 1.25 : 1) * (MVP ? 1.3 : 1) * (leader ? 1.2 : 1);
		let expMult = [1, 1.5, 2.0, 2.5, 3.0].map(x => x * buff); // Multi
		let levelsZip = zip([levelsCurrent, levelsTarget, expMult]);
		return (
			(MVP ? 2 : 1) * // MVP doubles the numbers of run
			levelsZip.reduce(
				(acc, [cur, tar, exp]) => acc + Math.ceil(xpIfOathed(cur, tar, oath) / (490 * 5 * exp)),
				0,
			)
		);
	}

	$: currentLevel = currentLevel > targetLevel ? targetLevel : currentLevel;
	$: levelDiff = targetLevel - currentLevel;
	$: xpToGain = xpIfOathed(currentLevel, targetLevel, oathed);
	$: runs = runsNb(currentLevel, targetLevel, oathed, event, command, leader, MVP);
</script>

<style>
	input {
		margin: auto;
		margin: 1rem;
	}

	.selected {
		background-color: #ff3e00;
		color: white;
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

<main>
	<button
		on:click={() => {
			info = !info;
		}}
		class:selected={info}>
		Infos
	</button>

	{#if info}
		<p>
			0-2 has 5 fights with <b>490 EXP</b> by fight, which makes it
			<b>2490 EXP</b>
			by run
		</p>
		<p>EXP gained is multiplied by 1 + (number of dummies * 0.5)</p>
	{/if}

	<div class="level-input">
		<h2>Current level</h2>
		<input type="number" min="1" max="120" bind:value={currentLevel} class="number" />
		<input type="range" min="1" max="120" list="levels" bind:value={currentLevel} class="range" />
	</div>

	<div class="level-input">
		<h2>Target level</h2>
		<input type="number" min="1" max="120" bind:value={targetLevel} class="number" />
		<input type="range" min="1" max="120" list="levels" bind:value={targetLevel} class="range" />
	</div>

	<datalist id="levels">
		<option value="1" label="1" />
		<option value="10" label="10" />
		<option value="30" label="30" />
		<option value="70" label="70" />
		<option value="90" label="90" />
		<option value="100" label="100" />
		<option value="110" label="110" />
		<option value="115" label="115" />
		<option value="120" label="120" />
	</datalist>

	<br />

	<label>
		<input type="checkbox" bind:checked={oathed} />
		<b>Oathed</b>
		(2.0x EXP multiplier when level > 100)
	</label>

	<label>
		<input type="checkbox" bind:checked={event} />
		<b>Exp Event</b>
		(1.5x EXP multiplier)
	</label>

	<br />

	<label>
		<input type="checkbox" bind:checked={command} />
		<b>Command Fairy</b>
		(1.25x EXP multiplier)
	</label>

	<label>
		<input type="checkbox" bind:checked={leader} />
		<b>Leader</b>
		(1.2x EXP multiplier)
	</label>

	<br />

	<label>
		<input type="checkbox" bind:checked={MVP} />
		<b>MVP</b>
		(1.3x EXP multiplier, doubles number of runs)
	</label>

	<hr />

	<p>Levels to gain: {levelDiff}</p>
	<p>XP to gain: {xpToGain}</p>
	<p class="reports">
		Number of runs:
		<b>{runs}</b>
	</p>
</main>
