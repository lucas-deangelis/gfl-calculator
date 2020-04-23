<script>
	let currentLevel = 1;
	let targetLevel = 90;
	let oathed = false;

	let xpByLevel = [
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

	$: currentLevel = currentLevel > targetLevel ? targetLevel : currentLevel;
	$: levelDifference = targetLevel - currentLevel;
	$: xpToGain = oathed ? ((xpByLevel[targetLevel-1] - xpByLevel[currentLevel-1]) / 2) : (xpByLevel[targetLevel-1] - xpByLevel[currentLevel-1]);
</script>

<main>
	<div class="level-input">
		<h2>Current level</h2>
		<input type="number" bind:value={currentLevel} class="number">
		<input type="range" min="1" max="120" list="levels" bind:value={currentLevel} class="range">
	</div>
	
	<div class="level-input">
		<h2>Target level</h2>
		<input type="number" bind:value={targetLevel} class="number">
		<input type="range" min="1" max="120" list="levels" bind:value={targetLevel} class="range">
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
		<input type="checkbox" bind:checked={oathed}>Oathed
	</label>

	<hr>

	<p>Level to gain: {levelDifference}</p>
	<p>XP to gain: {xpToGain}</p>
	<p class="reports">Combat reports: <b>{Math.ceil(xpToGain / 3000)}</b></p>
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
