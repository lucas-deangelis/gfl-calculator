<script>
	let currentLevel = 1;
	let targetLevel = 90;
	let oathed = false;

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

	// If current > target then return 0
	function xpDiff(current, target) {
		return Math.max(xpByLevel[target] - xpByLevel[current], 0);
	}

	function xpDivide(xp, double) {
		return Math.ceil(xp / (double ? 6000 : 3000));
	}

	function reportsExp(current, target, oath) {
		let xp1to100 = xpDiff(current, Math.min(target, 100));
		let xp100to120 = xpDiff(Math.max(current, 100), Math.min(target, 120));
		let reports1to100 = xpDivide(xp1to100, false);
		let reports100to120 = xpDivide(xp100to120, oath);

		return [xp1to100 + xp100to120, reports1to100 + reports100to120];
	}

	$: currentLevel = currentLevel > targetLevel ? targetLevel : currentLevel;
	$: levelDifference = targetLevel - currentLevel;
	$: [xpToGain, combatReports] = reportsExp(currentLevel, targetLevel, oathed);
</script>

<<<<<<< HEAD
<main>
	<div class="level-input">
    <h2>Current level</h2>
    <div class="level-box">
      <input type="number" min="1" max="120" bind:value={currentLevel} class="number">
      <input type="range" min="1" max="120" list="levels" bind:value={currentLevel} class="range">
    </div>
	</div>
	
	<div class="level-input">
		<h2>Target level</h2>
    <div class="level-box">
      <input type="number" min="1" max="120" bind:value={targetLevel} class="number">
      <input type="range" min="1" max="120" list="levels" bind:value={targetLevel} class="range">
    </div>
	</div>

	<datalist id="levels">
		<option value="1" label="1">
		<option value="10" label="10">
		<option value="30" label="30">
		<option value="70" label="70">
		<option value="90" label="90">
		<option value="100" label="100">
		<option value="110" label="110">
		<option value="115" label="115">
		<option value="120" label="120">
	</datalist>

	<br>
	
	<label>
		<input type="checkbox" bind:checked={oathed}>Oathed (doubles xp gain when level > 100)
	</label>

	<hr>

	<p>Levels to gain: {levelDifference}</p>
	<p>XP to gain: {xpToGain}</p>
	<p class="reports">Combat reports: <b>{combatReports}</b></p>
</main>

=======
>>>>>>> 360f245d05c561965ffa125ebfcf1748fbf24cd9
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

  .level-box {
    display: flex;
    flex-direction: column;
    justify-content: center;
  }

  @media (min-width: 640px) {
		.level-box {
			flex-direction: row;
		}
	}
</style>

<main>
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

	<hr />

	<p>Levels to gain: {levelDifference}</p>
	<p>XP to gain: {xpToGain}</p>
	<p class="reports">
		Combat reports:
		<b>{combatReports}</b>
	</p>
</main>
