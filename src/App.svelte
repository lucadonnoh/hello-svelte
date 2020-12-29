<script>
	import Nested from "./Nested.svelte";
	import FunnyPeople from "./FunnyPeople.svelte";

	let name = "Svelte!";

	let count = 0;
	$: doubled = count * 2;

	let logCount = 0;

	let logStress = 10;

	function incLogCount() {
		logCount += 1;
	}

	function handleClick() {
		count += 1;
	}

	let i = 0;
	
	function handleSecondClick() {
		i++;
		secondButtonPrompt = " click lol ora non puoi più";	
	}

	// reactivity is only triggered by assignements, so .push doesn't cause an update
	$: if (count >= 0) {
		console.log("the count is high af");
	}

	let user = { loggedIn: false };

	let dataLeak = "lol now i have all your data";

	function toggle() {
		if (logCount <= logStress * 2) {
			user.loggedIn = !user.loggedIn;
		} else {
			dataLeak = "ok i'm stopping this too";
		}

		if (logCount < logStress) {
			logState = user.loggedIn ? "Log Out" : "Log In";
		} else {
			logState = "for god's sake stop ping pongin this button";
		}

		incLogCount();
	}

	let logState = "Log In";

	let m = { x: 0, y: 0 };

	function handleMousemove(event) {
		m.x = event.clientX;
		m.y = event.clientY;
	}

	let secondButtonPrompt = "click";
</script>

<style>
	main {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}
	h1 {
		text-align: center;
		font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
			Oxygen, Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
		font-size: 2em;
	}

	.mouse {
		height: 100%;
		width: 100%;
		text-align: center;
	}
</style>

<main on:mousemove={handleMousemove}>
	<h1>Hello {name.toUpperCase()}</h1>
	<Nested curse="<strong>fuckin</strong>" />

	<p class="mouse">The mouse position is {m.x} x {m.y}</p>

	<button on:click={handleClick}>
		Clicked
		{count}
		{count === 1 ? 'time' : 'times'}
	</button>

	<p>and doubled is {doubled}</p>

	{#if user.loggedIn}
		<button on:click={toggle} disabled={logCount >= logStress * 3}>
			{logState}
		</button>
		<p>{dataLeak}</p>
	{:else}<button on:click={toggle}> {logState} </button>{/if}

	{#if logCount >= logStress * 3}
		<p>what about now</p>
		<FunnyPeople />

	<button on:click|once={handleSecondClick}>{i} {secondButtonPrompt}</button>
	{/if}

	<input type="number" bind:value={i}>

</main>
