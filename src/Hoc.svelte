<script>
	let currentLevel = 1;
	let targetLevel = 100;
	let rangeLevel = 10;
	let oathed = false;

	let xpByLevel = [0,500,1400,2700,4500,6700,9400,12600,16200,20200,24700,29700,35100,40900,47200,54000,61200,68800,77100,86100,95900,106500,118500,132000,147000,163500,181800,201900,223900,247900,274200,302500,333300,366600,402400,441000,482400,526600,574000,624600,678400,735700,796500,861000,929200,1001500,1077900,1158400,1243300,1332700,1426800,1525600,1629400,1738300,1852300,1971800,2096700,2227200,2363500,2505900,2654400,2809000,2970100,3137800,3312300,3493800,3682300,3877800,4080800,4291400,4509600,4735800,4970000,5212500,5463300,5722800,5990800,6267800,6553800,6849300,7154000,7468500,7792500,8127000,8471000,8826000,9191000,9567000,9954000,10352000,10761000,11182000,11614000,12058000,12514000,12983000,13464000,13957000,14463000,15000000];

	function reportsPerHour(rangeLevel) {
		if (rangeLevel == 10) {
			return 15;
		} else if (rangeLevel >= 9) {
			return 13;
		} else if (rangeLevel >= 7) {
			return 11;
		} else if (rangeLevel >= 6) {
			return 9;
		} else if (rangeLevel >= 4) {
			return 7;
		} else if (rangeLevel >= 3) {
			return 5;
		} else if (rangeLevel >= 1) {
			return 3;
		} else if (rangeLevel == 0) {
			return 1;
		}
	}

	$: currentLevel = currentLevel > targetLevel ? targetLevel : currentLevel;
	$: levelDifference = targetLevel - currentLevel;
	$: xpToGain = xpByLevel[targetLevel-1] - xpByLevel[currentLevel-1];
	$: combatReports = Math.ceil(xpToGain / 3000);
	$: batteries = 5 * Math.ceil(combatReports / reportsPerHour(rangeLevel));
</script>

<main>
	<div class="level-input">
		<h2>Current level</h2>
		<input type="number" bind:value={currentLevel} class="number">
		<input type="range" min="1" max="100" list="hoc-levels" bind:value={currentLevel} class="range">
	</div>
	
	<div class="level-input">
		<h2>Target level</h2>
		<input type="number" bind:value={targetLevel} class="number">
		<input type="range" min="1" max="100" list="hoc-levels" bind:value={targetLevel} class="range">
	</div>

	<div class="level-input">
		<h2>Training range level</h2>
		<input type="number" bind:value={rangeLevel} class="number">
		<input type="range" min="0" max="10" list="training-range-levels" bind:value={rangeLevel} class="range">
	</div>

	<datalist id="hoc-levels">
		<option value="1" label="1">
		<option value="20" label="10">
		<option value="40" label="30">
		<option value="60" label="70">
		<option value="100" label="100">
	</datalist>

	<datalist id="training-range-levels">
		<option value="0"></option>
		<option value="1"></option>
		<option value="3"></option>
		<option value="4"></option>
		<option value="6"></option>
		<option value="7"></option>
		<option value="9"></option>
		<option value="10"></option>
	</datalist>

	<br>
	
	<label>
		<input type="checkbox" bind:checked={oathed}>Oathed
	</label>

	{#if oathed}
		<p>You can't</p>
	{/if}

	<hr>

	<p>Level to gain: {levelDifference}</p>
	<p>XP to gain: {xpToGain}</p>
	<p class="reports">Special combat reports: <b>{combatReports}</b></p>
	<p class="batteries">Batteries: <b>{batteries}</b></p>
</main>

<style>
	input {
		margin: auto;
		margin: 1rem;
		
	}

	.range {
		width: 500px;
	}

	.reports {
		font-size: 1.5rem;
	}
</style>